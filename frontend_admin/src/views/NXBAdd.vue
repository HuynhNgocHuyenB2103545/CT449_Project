<template>
    <div>
        <div style="width: 60%;" class="mx-auto mt-5">
            <h4 class="text-center mb-2 text-success fw-bold">THÊM NHÀ XUẤT BẢN</h4>
            <NXBForm :nxb="nxb" :type="type" @submit:nxb="addNxb" />
        </div>
    </div>
</template>

<script>
import NXBForm from "@/components/NXBForm.vue";
import NxbService from "@/services/nxb.service.js";

export default {
    components: {
        NXBForm
    },
    data() {
        return {
            nxb: {
                maNxb: "",
                tenNxb: null,
                diaChi: null
            },
            type: "add",
        };

    },
    methods: {
        async addNxb(data) {
            try {
                await NxbService.create(data);
                alert("Thêm nhà xuất bản thành công");
            } catch (error) {
                console.log(error);
            }
        }
    },
};
</script>