<template>
    <div class="content px-3 border-3" style="margin: 20px auto;">
        <div v-if="this.success" class="text-center ">
            <p class="fs-4 pt-3 text-dark">{{ message }}</p>
            <router-link :to="{ path: '/login' }" class="btn btn-outline-success mb-2">Đăng Nhập</router-link>
        </div>
        <Form v-else @submit="register" :validation-schema="userFormSchema"
            style="margin: auto auto; background: #C9E4D6;" class="p-3 border rounded border-success">
            <div class="text-center my-2 fs-3 pb-2 text-success fw-bold">ĐĂNG KÝ</div>
            <div class="row">
                <div class="col-sm">
                    <div class="row mb-2 mx-2 px-3 pt-3">
                        <label for="username" class="col-sm-6 col-form-label fw-bold">Tên đăng nhập:</label>
                        <div class="col-sm">
                            <Field name="username" type="text" class="form-control" v-model="User.maDocGia" />
                            <ErrorMessage name="username" class="error-feedback" />
                        </div>
                    </div>
                    <div class="row mb-2 mx-2 px-3 pt-3">
                        <label for="password" class="col-sm-6 col-form-label fw-bold">Mật khẩu:</label>
                        <div class="col-sm">
                            <Field name="password" type="password" class="form-control" v-model="User.password" />
                            <ErrorMessage name="password" class="error-feedback" />
                        </div>
                    </div>
                    <div class="row mb-2 mx-2 px-3 pt-3">
                        <label for="confirm_password" class="col-sm-6 col-form-label fw-bold">Nhập lại mật khẩu:</label>
                        <div class="col-sm">
                            <Field name="confirm_password" type="password" class="form-control" />
                            <ErrorMessage name="confirm_password" class="error-feedback" />
                        </div>
                    </div>
                    <div class="row mb-2 mx-2 px-3 pt-3">
                        <label for="ho" class="col-sm-6 col-form-label fw-bold">Họ:</label>
                        <div class="col-sm">
                            <Field name="ho" type="text" class="form-control" v-model="User.hoLot" />
                            <ErrorMessage name="ho" class="error-feedback" />
                        </div>
                    </div>
                    <div class="row mb-2 mx-2 px-3 pt-3">
                        <label for="ten" class="col-sm-6 col-form-label fw-bold">Tên:</label>
                        <div class="col-sm">
                            <Field name="ten" type="text" class="form-control" v-model="User.ten" />
                            <ErrorMessage name="ten" class="error-feedback" />
                        </div>
                    </div>
                    <div class="row mb-2 mx-2 px-3 pt-3">
                        <label for="phai" class="col-sm-6 col-form-label fw-bold">Giới tính:</label>
                        <div class="col-sm">
                            <select name="phai" v-model="User.phai" class="form-select">
                                <option value="Nam">Nam</option>
                                <option value="Nữ">Nữ</option>
                            </select>
                            <ErrorMessage name="phai" class="error-feedback" />
                        </div>
                    </div>
                    <div class="row mb-2 mx-2 px-3 pt-3">
                        <label for="diachi" class="col-sm-6 col-form-label fw-bold">Địa chỉ:</label>
                        <div class="col-sm">
                            <Field name="diachi" type="text" class="form-control" v-model="User.diaChi" />
                            <ErrorMessage name="diachi" class="error-feedback" />
                        </div>
                    </div>
                    <div class="row mb-2 mx-2 px-3 pt-3">
                        <label for="sdt" class="col-sm-6 col-form-label fw-bold">Số điện thoại:</label>
                        <div class="col-sm">
                            <Field name="sdt" type="tel" class="form-control" v-model="User.dienThoai" />
                            <ErrorMessage name="sdt" class="error-feedback" />
                        </div>
                    </div>
                </div>
                
            </div>
            <p v-if="!this.success" class="ms-4 error-feedback">{{ message }}</p>
            <div>
                <button type="submit" class="col btn btn-outline-success ms-4 py-2">Đăng ký</button>
                <span class="ms-3">Bạn đã có tài khoản? <router-link :to="{ name: 'login' }">Đăng
                        Nhập</router-link></span>
            </div>
        </Form>
    </div>
</template>
<style scoped>
.error-feedback {
    color: red;
}
</style>
<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
import DocGiaService from "@/services/docgia.service";
export default {
    components: {
        Form,
        Field,
        ErrorMessage,
        DocGiaService
    },
    data() {
        const userFormSchema = yup.object().shape({
            username: yup
                .string()
                .required("Tên đăng nhập không được bỏ trống.")
                .min(4, "Tên đăng nhập phải ít nhất 4 ký tự.")
                .max(30, "Tên đăng nhập không quá 30 kí tự."),
            password: yup
                .string()
                .required("Mật khẩu không được bỏ trống.")
                .min(4, "Mật khẩu phải ít nhất 4 ký tự.")
                .max(20, "Mật khẩu tối đa 20 ký tự."),
            confirm_password: yup
                .string()
                .required("Mật khẩu xác nhận không được bỏ trống.")
                .min(4, "Mật khẩu phải ít nhất 4 ký tự.")
                .max(20, "Mật khẩu tối đa 20 ký tự.")
                .oneOf([yup.ref('password'), null], 'Mật khẩu xác nhận không khớp.'),
            ho: yup
                .string()
                .required("Tên không được bỏ trống.")
                .min(2, "Tên phải ít nhất 2 ký tự.")
                .max(50, "Tên có nhiều nhất 50 ký tự."),
            ten: yup
                .string()
                .required("Tên không được bỏ trống.")
                .min(2, "Tên phải ít nhất 2 ký tự.")
                .max(50, "Tên có nhiều nhất 50 ký tự."),
            diachi: yup
                .string()
                .required("Địa chỉ không được bỏ trống.")
                .max(100, "Địa chỉ tối đa 100 ký tự."),
            sdt: yup
                .string()
                .matches(
                    /((09|03|07|08|05)+([0-9]{8})\b)/g,
                    "Số điện thoại không hợp lệ."
                )
        });
        return {
            User: {
                maDocGia: "",
                password: "",
                hoLot: "",
                ten: "",
                phai: "Nam",
                diaChi: "",
                dienThoai: "",
            },
            userFormSchema,
            message: '',
            success: false,
        };
    },
    methods: {
        async register() {
            try {
                const result = await DocGiaService.create(this.User);
                this.success = true;
                this.message = "Đã đăng ký thành công!";
            } catch (error) {
                this.message = error.response.data.message;
            }
        },
    }
}
</script>