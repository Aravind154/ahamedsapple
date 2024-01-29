<template>
  <div class="full">
    <Header class="Header" />
    <div class="top">
      <div class="expected-date">
        <label for="chooseDate">Choose the Date</label>
        <input type="date" id="chooseDate" v-model="searchDate" @input="updateDate" class="custom-input" />
      </div>
      <div class="search-input">
        <span class="search-icon" @click="searchReport">&#128269;</span>
      </div>
    </div>
    <div class="table-container" id="no-more-tables">
      <table class="table">
        <thead>
          <tr>
            <th>Name</th>
            <th>PhoneNumber</th>
            <th>Gender</th>
            <th>Location</th>
            <th>Doctor Selection</th>
            <th>Finance</th>
            <th>Distance</th>
            <th>Treatment</th>
            <th>Expected Date</th>
            <th>Follow-up Date</th>
          </tr>
        </thead>
        <tbody>
          <tr v-if="source.length === 0">
            <td colspan="10" class="no-data-message">No data available</td>
          </tr>
          <tr v-else v-for="(item, index) in paginatedItems" :key="index">
            <td>{{ item.name }}</td>
            <td>{{ item.phonenumber }}</td>
            <td>{{ item.gender }}</td>
            <td>{{ item.location }}</td>
            <td>{{ item.doctorSelection }}</td>
            <td>{{ item.finance }}</td>
            <td>{{ item.distance }}</td>
            <td>{{ item.treatment }}</td>
            <td>{{ item.expectedDate }}</td>
            <td>{{ item.followUpDate }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <nav aria-label="Page navigation">
      <ul class="pagination">
        <li class="page-item">
          <a class="page-link" @click="changePage(pagination.page - 1)" href="#" :disabled="pagination.page === 1">
            &lt;
          </a>
        </li>
        <li class="page-item" :class="{ active: pagination.page === index + 1 }" v-for="(page, index) in totalPages"
          :key="index">
          <a class="page-link" @click="changePage(index + 1)" href="#">{{ index + 1 }}</a>
        </li>
        <li class="page-item">
          <a class="page-link" @click="changePage(pagination.page + 1)" href="#"
            :disabled="pagination.page === totalPages">
            &gt;
          </a>
        </li>
      </ul>
    </nav>
    <Footer />
  </div>
</template>

<script>
import Header from '~/components/Header.vue';
import { fetchDataForDate } from '~/api/api.js';

export default {
  components: {
    Header,
  },
  data() {
    return {
      searchDate: '', // Set to today's date by default
      defaultDate: '', // Added property to store today's date
      user: {
        name: "",
        objectId: '',
        loggedInUser: {},
      },
      source: [],
      pagination: {
        page: 1,
        itemsPerPage: 8,
      },
      // tableColumns: [
      //    'Name', 'PhoneNumber', 'Gender', 'Location', 'Doctor', 'Remarks', 'Doctor Selection', 'Follow-up Date'
      // ],
    };
  },
  mounted() {
    this.setDefaultDate();
    this.initUserData();
    this.fetchDataForDate(this.defaultDate)
      .then(() => {
        this.searchDate = this.defaultDate;
      })
      .catch((error) => {
        console.error('Error fetching data:', error);
      });
  },
  computed: {
    paginatedItems() {
      const start = (this.pagination.page - 1) * this.pagination.itemsPerPage;
      const end = start + this.pagination.itemsPerPage;
      return this.source.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.source.length / this.pagination.itemsPerPage);
    },
  },
  methods: {
    async searchReport() {
      this.fetchDataForDate(this.searchDate);
    },

    async fetchDataForDate(date) {
      try {
        this.validateObjectID();
        this.validateDate(date);

        const formattedDate = this.formatDate(date);
        const objectId = this.user.loggedInUser.objectId;

        this.source = await fetchDataForDate(objectId, formattedDate);
        this.pagination.page = 1;
      } catch (error) {
        console.error('Error fetching data:', error);
        throw error; // Re-throw the error for better error handling
      }
    },

    changePage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.pagination.page = page;
      }
    },

    updateDate(event) {
      this.searchDate = event.target.value;
    },

    setDefaultDate() {
      const today = new Date();
      const day = today.getDate().toString().padStart(2, '0');
      const month = (today.getMonth() + 1).toString().padStart(2, '0');
      const year = today.getFullYear();
      this.defaultDate = `${year}-${month}-${day}`;
      this.searchDate = this.defaultDate;
      console.log("Default Date:", this.defaultDate);
    },

    initUserData() {
      const storedUser = sessionStorage.getItem("loggedInUser");
      if (storedUser) {
        const sourceData = JSON.parse(JSON.parse(storedUser).source);
        this.user.loggedInUser = {
          name: sourceData.username,
          objectId: sourceData._id.$oid,
        };
        console.log("Logged-in user data:", this.user.loggedInUser);
      } else {
        console.log("No user data found in session storage.");
      }
    },

    validateObjectID() {
      if (!this.user.loggedInUser.objectId) {
        console.error('Object ID not found in the session');
        throw new Error('Object ID not found in the session');
      }
    },

    validateDate(date) {
      if (!date) {
        console.warn('Date is empty');
        throw new Error('Date is empty');
      }

      const parsedDate = new Date(date);

      if (isNaN(parsedDate.getTime())) {
        console.warn('Invalid date format');
        throw new Error('Invalid date format');
      }
    },

    formatDate(date) {
      const parsedDate = new Date(date);
      const day = parsedDate.getDate().toString().padStart(2, '0');
      const month = (parsedDate.getMonth() + 1).toString().padStart(2, '0');
      const year = parsedDate.getFullYear();
      return `${day}-${month}-${year}`;
    },
  },
};
</script>


<style scoped>
@import '@/styles/report.css';
</style>
