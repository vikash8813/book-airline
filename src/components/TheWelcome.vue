<script setup lang="ts">
import { ref } from 'vue'

const isOpen = ref(false)

const toggleMenu = () => {
  isOpen.value = !isOpen.value
}

const recommendedTrips = ref([
  {
    destination: 'New York, USA',
    price: 'From $350',
    image: 'https://source.unsplash.com/400x300/?newyork,city',
  },
  {
    destination: 'Paris, France',
    price: 'From $420',
    image: 'https://source.unsplash.com/400x300/?paris,eiffel-tower',
  },
  {
    destination: 'Tokyo, Japan',
    price: 'From $500',
    image: 'https://source.unsplash.com/400x300/?tokyo,japan',
  },
  {
    destination: 'Dubai, UAE',
    price: 'From $480',
    image: 'https://source.unsplash.com/400x300/?dubai,city',
  },
])
const reviews = ref([
  {
    name: "John Doe",
    rating: 5,
    comment: "Great service! Booking was fast and easy. Highly recommended.",
    avatar: "https://source.unsplash.com/50x50/?man,face",
  },
  {
    name: "Emma Watson",
    rating: 4,
    comment: "Had an amazing experience. Customer support was very helpful.",
    avatar: "https://source.unsplash.com/50x50/?woman,face",
  },
  {
    name: "Michael Smith",
    rating: 5,
    comment: "Best travel website! Found cheap flights quickly.",
    avatar: "https://source.unsplash.com/50x50/?man,portrait",
  },
  {
    name: "Sophia Brown",
    rating: 4,
    comment: "Smooth booking process, but I wish there were more payment options.",
    avatar: "https://source.unsplash.com/50x50/?woman,portrait",
  },
  {
    name: "David Johnson",
    rating: 5,
    comment: "Excellent deals! Will book again for my next trip.",
    avatar: "https://source.unsplash.com/50x50/?person,face",
  },
]);


const origin = ref('');
const destination = ref('');
const originCode = ref('NOU');
const destinationCode = ref('BKK');
const departDate = ref('');
const returnDate = ref('');
const passengers = ref(1);
const showHotels = ref(false);

const searchFlights = () => {
  console.log({
    origin: origin.value,
    destination: destination.value,
    departDate: departDate.value,
    returnDate: returnDate.value,
    passengers: passengers.value,
    showHotels: showHotels.value,
  });
};
</script>

<template>
  <nav class="bg-white shadow-md">
    <div class="container mx-auto px-4 py-3 flex justify-between items-center">
      <!-- Logo -->
      <a href="#" class="text-2xl font-bold text-blue-600">OneTravel</a>

      <!-- Desktop Menu -->
      <div class="hidden md:flex space-x-6">
        <a href="#" class="text-gray-700 hover:text-blue-500">Flights</a>
        <a href="#" class="text-gray-700 hover:text-blue-500">Hotels</a>
        <a href="#" class="text-gray-700 hover:text-blue-500">Cars</a>
        <a href="#" class="text-gray-700 hover:text-blue-500">Deals</a>
        <a href="#" class="text-gray-700 hover:text-blue-500">More</a>
      </div>

      <!-- Right Side -->
      <div class="flex items-center space-x-4">
        <a
          href="#"
          class="hidden md:block bg-blue-600 text-white px-4 py-2 rounded-md hover:bg-blue-700"
        >
          Sign In
        </a>

        <!-- Mobile Menu Button -->
        <button @click="toggleMenu" class="md:hidden focus:outline-none">
          <svg
            class="w-6 h-6 text-gray-700"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16m-7 6h7"
            />
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <div v-if="isOpen" class="md:hidden bg-white border-t p-4">
      <a href="#" class="block text-gray-700 py-2">Flights</a>
      <a href="#" class="block text-gray-700 py-2">Hotels</a>
      <a href="#" class="block text-gray-700 py-2">Cars</a>
      <a href="#" class="block text-gray-700 py-2">Deals</a>
      <a href="#" class="block text-gray-700 py-2">More</a>
      <a href="#" class="block bg-blue-600 text-white text-center py-2 rounded-md mt-2">Sign In</a>
    </div>
  </nav>

  <div>
    <section class="bg-blue-600 text-white  py-16">

      <div class="container mx-auto text-center">
        <h1 class="text-4xl font-bold">Search and Book Cheap Flights</h1>
        <p class="mt-2 text-lg">Find the best deals on flights worldwide</p>


      </div>
      <div class="flex items-center justify-center mt-5">
        <div class="bg-white shadow-lg rounded-lg p-4 md:p-6 w-full max-w-4xl">
          <form class="grid grid-cols-1 md:grid-cols-6 gap-4">
            <!-- Origin -->
            <div class="col-span-1 md:col-span-2">
              <label class="block text-gray-600 text-sm font-medium">Origin</label>
              <div class="relative flex items-center border border-gray-300 rounded-lg p-2">
                <input type="text" v-model="origin" placeholder="Enter city" class="w-full focus:outline-none">
                <span class="ml-2 text-gray-500 text-sm">{{ originCode }}</span>
              </div>
            </div>

            <!-- Destination -->
            <div class="col-span-1 md:col-span-2">
              <label class="block text-gray-600 text-sm font-medium">Destination</label>
              <div class="relative flex items-center border border-gray-300 rounded-lg p-2">
                <input type="text" v-model="destination" placeholder="Enter city" class="w-full focus:outline-none">
                <span class="ml-2 text-gray-500 text-sm">{{ destinationCode }}</span>
              </div>
            </div>

            <!-- Depart Date -->
            <div class="col-span-1">
              <label class="block text-gray-600 text-sm font-medium">Depart date</label>
              <div class="relative flex items-center border border-gray-300 rounded-lg p-2">
                <input type="date" v-model="departDate" class="w-full focus:outline-none">
              </div>
            </div>

            <!-- Return Date -->
            <div class="col-span-1">
              <label class="block text-gray-600 text-sm font-medium">Return date</label>
              <div class="relative flex items-center border border-gray-300 rounded-lg p-2">
                <input type="date" v-model="returnDate" class="w-full focus:outline-none">
                <!--              <button @click="returnDate = ''" class="ml-2 text-gray-400 hover:text-red-500">&times;</button>-->
              </div>
            </div>

            <!-- Passengers -->
            <div class="col-span-1">
              <label class="block text-gray-600 text-sm font-medium">Passengers</label>
              <select v-model="passengers" class="border border-gray-300 rounded-lg p-2 w-full">
                <option v-for="num in 10" :key="num">{{ num }} passenger</option>
              </select>
            </div>

            <!-- Search Button -->
            <div class="col-span-1 flex items-end">
              <button @click.prevent="searchFlights" class="bg-blue-600 text-white px-6 py-2 rounded-lg w-full hover:bg-blue-700 transition">
                Search
              </button>
            </div>
          </form>

          <!-- Show Hotels Checkbox -->
          <!--          <div class="flex items-center mt-4">-->
          <!--            <input type="checkbox" v-model="showHotels" class="mr-2">-->
          <!--            <label class="text-gray-600">Show hotels</label>-->
          <!--          </div>-->
        </div>
      </div>
    </section>
  </div>

  <div>
    <section class="py-16">
      <div class="container mx-auto text-center">
        <h2 class="text-3xl font-bold">Top Travel Deals</h2>

        <div class="mt-6 grid grid-cols-1 md:grid-cols-3 gap-6">
          <div class="bg-white p-4 shadow-md rounded-md">
            <h3 class="text-xl font-semibold">New York → London</h3>
            <p class="text-gray-600">Starting from $350</p>
            <button class="bg-blue-600 text-white px-4 py-2 mt-4">Book Now</button>
          </div>
          <div class="bg-white p-4 shadow-md rounded-md">
            <h3 class="text-xl font-semibold">Los Angeles → Tokyo</h3>
            <p class="text-gray-600">Starting from $500</p>
            <button class="bg-blue-600 text-white px-4 py-2 mt-4">Book Now</button>
          </div>
          <div class="bg-white p-4 shadow-md rounded-md">
            <h3 class="text-xl font-semibold">Paris → Dubai</h3>
            <p class="text-gray-600">Starting from $420</p>
            <button class="bg-blue-600 text-white px-4 py-2 mt-4">Book Now</button>
          </div>
        </div>
      </div>
    </section>
  </div>

  <div>
    <section class="py-16 bg-gray-100">
      <div class="container mx-auto">
        <h2 class="text-3xl font-bold text-center mb-8">Recommended for your next trip</h2>

        <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-6">
          <div
            v-for="(trip, index) in recommendedTrips"
            :key="index"
            class="bg-white rounded-lg shadow-md overflow-hidden"
          >
            <img :src="trip.image" :alt="trip.destination" class="w-full h-48 object-cover" />
            <div class="p-4">
              <h3 class="text-xl font-semibold">{{ trip.destination }}</h3>
              <p class="text-gray-600">{{ trip.price }}</p>
              <button
                class="bg-blue-600 text-white px-4 py-2 mt-4 w-full rounded-md hover:bg-blue-700"
              >
                Book Now
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>

  <div>
    <section class="py-16 bg-white">
      <div class="container mx-auto">
        <h2 class="text-3xl font-bold text-center mb-8">What Our Customers Say About Our Service?</h2>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div v-for="(review, index) in reviews" :key="index" class="bg-gray-100 p-6 rounded-lg shadow-md">
            <div class="flex items-center space-x-4">
              <img :src="review.avatar" alt="User Avatar" class="w-12 h-12 rounded-full">
              <div>
                <h3 class="text-lg font-semibold">{{ review.name }}</h3>
                <p class="text-yellow-500 flex">
                <span v-for="star in 5" :key="star">
                  <svg v-if="star <= review.rating" class="w-5 h-5 fill-current text-yellow-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
                    <path d="M10 15.27L16.18 19l-1.64-7.03L20 7.24l-7.19-.61L10 0 7.19 6.63 0 7.24l5.46 4.73L3.82 19z"/>
                  </svg>
                </span>
                </p>
              </div>
            </div>
            <p class="mt-4 text-gray-600">"{{ review.comment }}"</p>
          </div>
        </div>
      </div>
    </section>
  </div>

  <div>
    <footer class="bg-gray-900 text-white py-8">
      <div class="container mx-auto px-6">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <!-- Company Info -->
          <div>
            <h2 class="text-2xl font-semibold">OneTravel</h2>
            <p class="mt-2 text-gray-400">Your trusted travel partner for the best deals on flights, hotels, and more.</p>
          </div>

          <!-- Quick Links -->
          <div>
            <h3 class="text-xl font-semibold">Quick Links</h3>
            <ul class="mt-2 space-y-2">
              <li><a href="#" class="hover:text-blue-400">Home</a></li>
              <li><a href="#" class="hover:text-blue-400">Flights</a></li>
              <li><a href="#" class="hover:text-blue-400">Hotels</a></li>
              <li><a href="#" class="hover:text-blue-400">Contact Us</a></li>
            </ul>
          </div>

          <!-- Social Media -->
          <div>
            <h3 class="text-xl font-semibold">Follow Us</h3>
            <div class="flex space-x-4 mt-2">
              <a href="#" class="text-gray-400 hover:text-blue-400">
                <i class="fab fa-facebook text-2xl"></i>
              </a>
              <a href="#" class="text-gray-400 hover:text-blue-400">
                <i class="fab fa-twitter text-2xl"></i>
              </a>
              <a href="#" class="text-gray-400 hover:text-blue-400">
                <i class="fab fa-instagram text-2xl"></i>
              </a>
              <a href="#" class="text-gray-400 hover:text-blue-400">
                <i class="fab fa-linkedin text-2xl"></i>
              </a>
            </div>
          </div>
        </div>

        <div class="border-t border-gray-700 mt-6 pt-4 text-center text-gray-400">
          <p>© {{ new Date().getFullYear() }} OneTravel. All rights reserved.</p>
        </div>
      </div>
    </footer>
  </div>
  <div>

  </div>
</template>
