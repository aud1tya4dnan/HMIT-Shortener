<template>
    <div class="container">
        <div id="search" class="">
            <input type="text" @keypress.enter="search()" v-model="search" placeholder="Search" class="w-1/2 p-2 border border-gray-300 rounded-lg">
        </div>

        <div class="overflow-x-auto"> <!-- table -->
            <table class="min-w-full divide-y-2 divide-gray-200 bg-white text-sm dark:divide-gray-700 dark:bg-gray-900">
                <thead class="ltr:text-left rtl:text-right">
                    <tr>
                        <th class="whitespace-nowrap px-4 py-2 font-medium text-gray-900 dark:text-white">Shortlink</th>
                        <th class="whitespace-nowrap px-4 py-2 font-medium text-gray-900 dark:text-white">
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
                        <td class="whitespace-nowrap px-4 py-2 font-medium text-gray-900 dark:text-white">
                            John Doe
                        </td>
                        <td class="whitespace-nowrap px-4 py-2 text-gray-700 dark:text-gray-200">24/05/1995</td>
                        <td class="whitespace-nowrap px-4 py-2 text-gray-700 dark:text-gray-200">Web Developer</td>
                        <td class="whitespace-nowrap px-4 py-2 text-gray-700 dark:text-gray-200">$120,000</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import axios from 'axios';


export default {
    data() {
        return {
            links: [],
            flink: "",
            slink: "",
            userID: "",
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
            let uid = localStorage.getItem('uid');

        }
    }
}
</script>