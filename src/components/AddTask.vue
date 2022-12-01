<template>
    <form @submit="onSubmit" action="">
        <section class="">
            <div class="space-y-2 pb-4">
                <label class="block" for="text">Task Name</label>
                <input v-model="text" class="border border-gray-400 p-2 w-full rounded-md" type="text" name="text"
                    id="text" />
            </div>

            <div class="space-y-2">
                <label class="block" for="day">Day & Time</label>
                <input v-model="day" class="border border-gray-400 p-2 w-full rounded-md" type="datetime-local" name="day"
                    id="day" />
            </div>

            <div class="mt-4">
                <label for="reminder">Set Reminder?</label>
                <input v-model="reminder" type="checkbox" name="reminder" id="reminder" class="ml-4" />
            </div>

            <div class="py-4">
                <Button class="bg-green-500 text-white p-2 rounded-md w-full" text="Save Task" />
            </div>
        </section>
    </form>
</template>

<script>
import Button from "./Button.vue";

export default {
    name: "AddTask",

    data() {
        return {
            text: "",
            day: "",
            reminder: false,
        };
    },

    methods: {
        onSubmit(e) {
            e.preventDefault();
            if (!this.text) {
                alert("please add a task");
                return;
            }

            const newTask = {
                // id: Math.floor(Math.random() * 1000000),
                text: this.text,
                day: this.day,
                reminder: this.reminder,
            };

            this.$emit("add-task", newTask);

            this.text = "";
            this.day = "";
            this.reminder = "";
        },
    },

    components: {
        Button,
    },
};
</script>
