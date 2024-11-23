<script setup lang="ts" generic="T">
type DataTableWidth = number | 'auto';
type DataTableFormat = (value: any) => string;

export type DataTableColumn<T> = {
    field: keyof T;
    alignment?: string;
    width?: DataTableWidth;
    format?: DataTableFormat;
};

export type DataTableFooter = {
    name: string;
    value: any;
    format?: DataTableFormat;
};

type DateTableProps<T = any> = {
    columns: DataTableColumn<T>[];
    items: T[];
    footers: DataTableFooter[];
};

defineProps<DateTableProps<T>>();

function alignment(alignment: string | undefined) {
    if (!alignment) {
        return 'text-left';
    }
    return `text-${alignment}`;
}

function width(width: DataTableWidth | undefined): string {
    if (width === undefined) {
        return 'flex-1';
    }
    return `w-[${width}px]`;
}

function format(value: any, format: DataTableFormat | undefined): any {
    if (!format) {
        return value;
    }
    return format(value);
}
</script>

<template>
    <div class="flex flex-col gap-y-4">
        <div class="flex flex-col gap-y-4">
            <div class="flex" v-for="(item, index) in items" :key="index">
                <div
                    v-for="(column, index) in columns"
                    :key="index"
                    :class="[alignment(column.alignment), width(column.width)]"
                >
                    {{ format(item[column.field], column.format) }}
                </div>
            </div>
        </div>
        <hr />
        <div class="flex flex-col gap-y-4">
            <div v-for="(footer, index) in footers" :key="index" class="flex">
                <div class="flex-1 uppercase text-gray-400">
                    {{ footer.name }}
                </div>
                <div class="flex-0 text-right">
                    {{ format(footer.value, footer.format) }}
                </div>
            </div>
        </div>
    </div>
</template>
