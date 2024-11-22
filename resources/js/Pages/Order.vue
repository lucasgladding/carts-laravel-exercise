<script setup lang="ts">
import CustomLayout from '@/Layouts/CustomLayout.vue';
import { Head } from '@inertiajs/vue3';
</script>

<template>
    <Head title="Order"></Head>

    <CustomLayout>
        <div class="flex w-[1200px]">
            <div class="w-1/3 border-r">
                <h2 class="bg-blue-600 p-4 uppercase text-white">
                    Delivering to
                </h2>

                <div class="flex flex-col gap-4 p-4">
                    <div>
                        <div class="uppercase text-gray-400">Recipient</div>
                        <div>John Smith</div>
                    </div>

                    <div>
                        <div class="uppercase text-gray-400">Address</div>
                        <address>
                            123 Main Street<br />
                            Waterloo, Ontario, Canada<br />
                            A1B 2C3
                        </address>
                    </div>

                    <hr class="-mx-4" />

                    <div>
                        <div class="uppercase text-gray-400">
                            Special instructions
                        </div>
                        <div>Lorem ipsum</div>
                    </div>
                </div>
            </div>

            <div class="w-2/3">
                <h2 class="bg-blue-600 p-4 uppercase text-white">Your order</h2>

                <div class="p-4">
                    <table class="w-full">
                        <thead class="bg-gray-200">
                            <tr>
                                <td class="px-4 py-2">Quantity</td>
                                <td class="px-4 py-2">Product</td>
                                <td class="px-4 py-2">Cost</td>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td class="px-4 py-2">1</td>
                                <td class="px-4 py-2">Logitech MX mouse</td>
                                <td class="px-4 py-2">$49.95</td>
                            </tr>
                            <tr class="border-t">
                                <td class="px-4 py-2" colspan="2">Subtotal</td>
                                <td class="px-4 py-2">$49.95</td>
                            </tr>
                            <tr>
                                <td class="px-4 py-2" colspan="2">Taxes</td>
                                <td class="px-4 py-2">5.00</td>
                            </tr>
                            <tr class="border-b">
                                <td class="px-4 py-2" colspan="2">Shipping</td>
                                <td class="px-4 py-2">5.00</td>
                            </tr>
                            <tr>
                                <td class="px-4 py-2" colspan="2">Total</td>
                                <td class="px-4 py-2">$75.00</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </CustomLayout>
</template>
