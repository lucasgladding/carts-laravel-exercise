<script setup lang="ts" generic="T">
export type DataTableColumn<T> = {
    field: keyof T;
};

export type DataTableFooter = {
    name: string;
    value: any;
};

type DateTableProps<T = any> = {
    columns: DataTableColumn<T>[];
    items: T[];
    footers: DataTableFooter[];
};

defineProps<DateTableProps<T>>();
</script>

<template>
    <div class="flex flex-col gap-y-4">
        <div class="flex flex-col gap-y-4">
            <div class="flex" v-for="(item, index) in items" :key="index">
                <div v-for="(column, index) in columns" :key="index">
                    <div>
                        {{ item[column.field] }}
                    </div>
                </div>
            </div>
        </div>
        <hr />
        <div class="flex flex-col gap-y-4">
            <div v-for="(footer, index) in footers" :key="index" class="flex">
                <div class="flex-1">{{ footer.name }}</div>
                <div class="flex-0 text-right">
                    {{ footer.value }}
                </div>
            </div>
        </div>
    </div>
</template>
