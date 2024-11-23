<script setup lang="ts">
import DataTable, {
    DataTableColumn,
    DataTableFooter,
} from '@/Components/DataTable.vue';
import CustomLayout from '@/Layouts/CustomLayout.vue';
import { Head } from '@inertiajs/vue3';
import { computed } from 'vue';

const TAX_RATE = 0.15;

type OrderLine = {
    quantity: number;
    product: string;
    cost: number;
};

const columns: DataTableColumn<OrderLine>[] = [
    { field: 'product' },
    { field: 'quantity' },
    { field: 'cost' },
];

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
        style: 'decimal',
        minimumFractionDigits: 2,
        maximumFractionDigits: 2,
    });
    return format.format(amount);
}

const footers: DataTableFooter[] = computed(() => [
    { name: 'Subtotal', value: subtotal.value },
    { name: 'Taxes', value: taxes.value },
    { name: 'Shipping', value: shipping.value },
    { name: 'Total', value: total.value },
]);
</script>

<template>
    <Head title="Order"></Head>

    <CustomLayout>
        <div class="p-6">
            <h1 class="mb-6 text-5xl font-bold">Your Order</h1>

            <div class="flex w-[1200px]">
                <div class="w-1/3">
                    <h2 class="bg-black p-4 uppercase text-white">
                        Delivering to
                    </h2>

                    <div class="flex flex-col gap-4 p-4">
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

                        <hr />

                        <div>
                            <div class="uppercase text-gray-400">
                                Special instructions
                            </div>
                            <div>Lorem ipsum</div>
                        </div>
                    </div>
                </div>

                <div class="w-2/3">
                    <h2 class="bg-black p-4 uppercase text-white">
                        Your order
                    </h2>

                    <DataTable
                        class="p-4"
                        :columns="columns"
                        :items="lines"
                        :footers="footers"
                    />
                </div>
            </div>
        </div>
    </CustomLayout>
</template>
