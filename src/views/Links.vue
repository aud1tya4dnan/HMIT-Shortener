<template>
    <div class="container">
        <div id="search" class="place-self-center">
            <input type="text" @keypress.enter="search()" v-model="search" placeholder="Search" class="w-1/2 p-2 border border-gray-300 rounded-lg">
        </div>

        <div class="overflow-x-auto"> <!-- table -->
            <table class="min-w-full divide-y-2 divide-gray-200 bg-white text-sm dark:divide-gray-700 dark:bg-gray-900">
                <thead class="ltr:text-left rtl:text-right">
                    <tr>
                        <th class="whitespace-nowrap px-3 py-2 font-medium text-gray-900 dark:text-white">Shortlink</th>
                        <th class="whitespace-nowrap px-2 py-2 font-medium text-gray-900 dark:text-white">
                            Redirects To
                        </th>
                        <th class="whitespace-nowrap px-4 py-2 font-medium text-gray-900 dark:text-white">Edit</th>
                        <th class="whitespace-nowrap px-4 py-2 font-medium text-gray-900 dark:text-white">
                            Delete
                        </th>
                    </tr>
                </thead>

                <tbody class="divide-y divide-gray-200 dark:divide-gray-700" v-for="link in links" :key="link">
                    <tr>
                        <td class="whitespace-nowrap px-4 py-2 font-medium"  >
                            <a :href="'http://localhost:5173/' + link.slink">{{ link.slink }}</a>
                        </td>
                        <td class="whitespace-nowrap px-4 py-2 "><a :href="link.flink">Open the Link</a></td>
                        <td class="whitespace-nowrap px-4 py-2 "><button>Edit</button></td>
                        <td class="whitespace-nowrap px-4 py-2 "><button>Delete</button></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import api from '../api/url.js'


export default {
    data() {
        return {
            links: [],
            flink: "",
            slink: "",
            userID: "",
            search: "",
            newLink: [
                {
                    id: "",
                    newslink: "",
                    newflink: "",
                },
            ],
            editbar: false,
        };

    },
    methods: {
        async getLink() {
            this.userID = sessionStorage.getItem('uid');
            try {
                const res = await axios
                    .get( api + "link/" + this.userID)
                    .then((res) => {
                        this.links = res.data;
                    })
            } catch (error) {
                console.log(error);
            }
        },
        async search() {
            try {
                const res = await axios
                    .get( api + "search/" + this.search)
                    .then((res) => {
                        this.links = res.data;
                    })
            } catch (error) {
                console.log(error);
            }
        }
    },
    mounted(){
        this.getLink();
    }
}
</script>