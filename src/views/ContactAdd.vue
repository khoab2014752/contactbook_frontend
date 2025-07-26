 
<template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="createContact" />
        <p>{{ message }}</p>
        
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: null,
            message: "",
        };
    },
    methods: {
        async getContact() {
            this.contact = {
                "name": "",
                "email": "",
                "address": "",
                "phone": "",
                "favorite": true
            };
        },
        async createContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Thêm liên hệ thành công.";
                console.log(data);
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.getContact();
        this.message = "";
    },
};
</script>