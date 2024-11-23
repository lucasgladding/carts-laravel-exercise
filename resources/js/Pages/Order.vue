<script setup lang="ts">
import CustomLayout from '@/Layouts/CustomLayout.vue';
import { Head } from '@inertiajs/vue3';
import { computed } from 'vue';

type OrderLine = {
    quantity: number;
    product: string;
    cost: number;
};

const TAX_RATE = 0.1;

const lines: OrderLine[] = [
    {
        quantity: 1,
        product: 'Logitech MX',
        cost: 49.95,
    },
    {
        quantity: 2,
        product: 'Logitech MX',
        cost: 49.95,
    },
];

const subtotal = computed(() => {
    return lines.reduce((output, line) => {
        return output + line.cost * line.quantity;
    }, 0);
});

const taxes = computed(() => {
    return subtotal.value * TAX_RATE;
});

const shipping = computed(() => {
    return lines.length * 5;
});

const total = computed(() => {
    return subtotal.value + taxes.value + shipping.value;
});

function formatAmount(amount: number) {
    const format = Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
        minimumFractionDigits: 2,
        maximumFractionDigits: 2,
    });
    return format.format(amount);
}
</script>

<template>
    <Head title="Order"></Head>

    <CustomLayout>
        <div class="p-6">
            <h1 class="mb-6 text-5xl font-bold">Your Order</h1>

            <div class="flex w-[1200px]">
                <div class="w-1/3">
                    <h2 class="bg-blue-600 p-6 uppercase text-white">
                        Delivering to
                    </h2>

                    <div class="flex flex-col gap-4 p-6">
                        <div>
                            <div class="uppercase text-gray-400">Recipient</div>
                            <div>John Smith</div>
                        </div>

                        <div>
                            <div class="uppercase text-gray-400">Address</div>
                            <address class="not-italic">
                                123 Main Street<br />
                                Waterloo, Ontario, Canada<br />
                                A1B 2C3
                            </address>
                        </div>

                        <hr class="-mx-6" />

                        <div>
                            <div class="uppercase text-gray-400">
                                Special instructions
                            </div>
                            <div>Lorem ipsum</div>
                        </div>
                    </div>
                </div>

                <div class="w-2/3">
                    <h2 class="bg-blue-600 p-6 uppercase text-white">
                        Your order
                    </h2>

                    <div class="p-6">
                        <table class="w-full border">
                            <thead class="bg-gray-200">
                                <tr>
                                    <td
                                        class="px-4 py-2 uppercase text-gray-400"
                                    >
                                        Quantity
                                    </td>
                                    <td
                                        class="px-4 py-2 uppercase text-gray-400"
                                    >
                                        Product
                                    </td>
                                    <td
                                        class="px-4 py-2 text-right uppercase text-gray-400"
                                    >
                                        Cost
                                    </td>
                                </tr>
                            </thead>
                            <tbody>
                                <tr
                                    class="border-b"
                                    v-for="(line, index) in lines"
                                    :key="index"
                                >
                                    <td class="px-4 py-2">
                                        {{ line.quantity }}
                                    </td>
                                    <td class="px-4 py-2">
                                        {{ line.product }}
                                    </td>
                                    <td class="px-4 py-2 text-right">
                                        {{ formatAmount(line.cost) }}
                                    </td>
                                </tr>
                                <tr class="border-b">
                                    <td class="px-4 py-2" colspan="2">
                                        Subtotal
                                    </td>
                                    <td class="px-4 py-2 text-right">
                                        {{ formatAmount(subtotal) }}
                                    </td>
                                </tr>
                                <tr class="border-b">
                                    <td class="px-4 py-2" colspan="2">Taxes</td>
                                    <td class="px-4 py-2 text-right">
                                        {{ formatAmount(taxes) }}
                                    </td>
                                </tr>
                                <tr class="border-b">
                                    <td class="px-4 py-2" colspan="2">
                                        Shipping
                                    </td>
                                    <td class="px-4 py-2 text-right">
                                        {{ formatAmount(shipping) }}
                                    </td>
                                </tr>
                                <tr class="">
                                    <td class="px-4 py-2" colspan="2">Total</td>
                                    <td class="px-4 py-2 text-right">
                                        {{ formatAmount(total) }}
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </CustomLayout>
</template>
