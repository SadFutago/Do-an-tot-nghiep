<template>
    <div class="admin-page">
        <div class="admin-content">
            <div class="admin-content__heading">
                <h3>Trang chủ</h3>
            </div>
            <!-- admin card -->
            <div class="admin-content__card-mold">
                <div class="bg-blue admin-content__card">
                    <div class="admin-content__card-body">
                        <div class="admin-content__card-text">
                            <h3>150</h3>
                            <p>New Orders</p>
                        </div>
                        <i class="dark-blue admin-content__card-icon fa-solid fa-bag-shopping"></i>
                    </div>
                    <a href="#" class="admin-content__card-link white bg-dark-blue">
                        <p>Xem thêm</p>
                        <i class="fa-solid fa-circle-arrow-right"></i>
                    </a>
                </div>
                <div class="bg-green admin-content__card">
                    <div class="admin-content__card-body">
                        <div class="admin-content__card-text">
                            <h3>50%</h3>
                            <p>Bounce Rate</p>
                        </div>
                        <i class="dark-green admin-content__card-icon fa-solid fa-bag-shopping"></i>
                    </div>
                    <a href="#" class="admin-content__card-link white bg-dark-green">
                        <p>Xem thêm</p>
                        <i class="fa-solid fa-circle-arrow-right"></i>
                    </a>
                </div>
                <div class="bg-yellow admin-content__card">
                    <div class="admin-content__card-body">
                        <div class="black admin-content__card-text">
                            <h3>150</h3>
                            <p>New Orders</p>
                        </div>
                        <i class="dark-yellow admin-content__card-icon fa-solid fa-bag-shopping"></i>
                    </div>
                    <a href="#" class="admin-content__card-link black bg-dark-yellow">
                        <p>Xem thêm</p>
                        <i class="fa-solid fa-circle-arrow-right"></i>
                    </a>
                </div>
                <div class="bg-red admin-content__card">
                    <div class="admin-content__card-body">
                        <div class="admin-content__card-text">
                            <h3>150</h3>
                            <p>New Orders</p>
                        </div>
                        <i class="dark-red admin-content__card-icon fa-solid fa-bag-shopping"></i>
                    </div>
                    <a href="#" class="admin-content__card-link white bg-dark-red">
                        <p>Xem thêm</p>
                        <i class="fa-solid fa-circle-arrow-right"></i>
                    </a>
                </div>
            </div>
            <!-- chart -->
            <div class="admin-content__chart-mold">
                <div class="admin-content__chart">
                    <LineChart :chartData="lineData" :chartOptions="chartOptions"/>
                </div>
                <div class="admin-content__form-divided">
                    <div class="admin-content__chart">
                        <BarChart :chartData="barData" :chartOptions="chartOptions"/>
                    </div>
                    <div class="admin-content__chart">
                        <DoughnutChart :chartData="doughnutData" :chartOptions="chartOptions"/>
                    </div>
                </div>
            </div>
            <!-- table -->
            <div class="admin-content__table">
                <div class="admin-content__header d-flex align-items-center">
                    <h4>Sản phẩm bán chạy</h4>
                    <select id="selectCheckboxAction" class="form-select admin-content__checkbox-select-all-opts" @change="renderSelectChange">
                        <option value="" selected>-- Hành động --</option>
                        <option value="delete">Xóa</option>
                        <option value="addCategory">Thêm danh mục</option>
                        <option value="removeCategory">Xóa danh mục</option>
                        <option value="setPromotion">Đặt khuyến mãi</option>
                        <option value="setStatus">Đặt trạng thái</option>
                        <option value="filterByCategory">Lọc theo danh mục</option>
                        <option value="filterByPromotion">Lọc theo khuyến mãi</option>
                        <option value="filterByStatus">Lọc theo trạng thái</option>
                    </select>
                    <select id="selectedCategory" class="form-select admin-content__select-attribute admin-content__select-category">
                        <option value="" selected>-- Chọn danh mục --</option>
                        <option v-for="category in categories" :key="category._id" :value="category._id">
                            {{ category.name }}
                        </option>
                    </select>
                    <select id="selectedPromotion" class="form-select admin-content__select-attribute admin-content__select-promotion">
                        <option value="" selected>-- Chọn khuyến mãi --</option>
                        <option v-for="promotion in promotions" :key="promotion._id" :value="promotion._id">
                            {{ promotion.name }}
                        </option>
                    </select>
                    <select id="selectedStatus" class="form-select admin-content__select-status">
                        <option value="" selected>-- Chọn trạng thái --</option>
                        <option v-for="(label, value) in statusOptions" :key="value" :value="value">
                            {{ label }}
                        </option>
                    </select>
                    <button class="fs-16 btn btn-primary disabled" id="btnCheckboxSubmit" @click="btnCheckboxSubmitClicked()">Thực hiện</button>
                </div>
                <table class="table admin-content__table-main">
                    <thead class="admin-content__table-main-head">
                        <tr class="admin-content__table-first-row">
                            <th scope="col">
                                <input class="form-check-input admin-content__checkbox" type="checkbox" ref="checkboxAll" @change="onCheckboxAllChange($event)">
                            </th>
                            <th scope="col">ID
                                <SortComponent field="_id" :sort="sort"/>
                            </th>
                            <th scope="col">Tên
                                <SortComponent field="username" :sort="sort"/>
                            </th>
                            <th scope="col">Danh mục
                                <SortComponent field="categoryId" :sort="sort"/>
                            </th>
                            <th scope="col">Nhà cung cấp
                                <SortComponent field="supplierId" :sort="sort"/>
                            </th>
                            <th scope="col">Giá
                                <SortComponent field="listPrice" :sort="sort"/>
                            </th>
                            <th scope="col">Khuyến mãi
                                <SortComponent field="promotionId" :sort="sort"/>
                            </th>
                            <th scope="col">Số lượng
                                <SortComponent field="quantity" :sort="sort"/>
                            </th>
                            <th scope="col">Đơn vị tính
                                <SortComponent field="unitId" :sort="sort"/>
                            </th>
                            <th scope="col">Ngày tạo
                                <SortComponent field="createdAt" :sort="sort"/>
                            </th>
                            <th scope="col">Ngày cập nhật
                                <SortComponent field="updatedAt" :sort="sort"/>
                            </th>
                            <th scope="col">Trạng thái
                                <SortComponent field="status" :sort="sort"/>
                            </th>
                            <th scope="col" class="col-2"></th>
                        </tr>
                    </thead>
                    <tbody class="admin-content__table-main-body">
                        <template v-if="autoParts">
                            <tr class="admin-content__table-row" v-for="autoPart in autoParts" :key="autoPart._id">
                                <th>
                                    <input class="form-check-input" type="checkbox" ref="checkboxes" :value="autoPart._id" @change="onCheckboxChange()">
                                </th>
                                <th>{{ autoPart._id }}</th>
                                <td>{{ autoPart.name }}</td>
                                <td>{{ autoPart.category }}</td>
                                <td>{{ autoPart.supplier }}</td>
                                <td>{{ autoPart.listPrice }}</td>
                                <td>{{ autoPart.promotion }}</td>
                                <td>{{ autoPart.quantity }}</td>
                                <td>{{ autoPart.unit }}</td>
                                <td>{{ autoPart.createdAt }}</td>
                                <td>{{ autoPart.updatedAt }}</td>
                                <td>{{ autoPart.status }}</td>
                                <td>
                                    <router-link :to="'/admin/autoPart/edit/' + autoPart._id" class="fs-16 btn btn-primary">Sửa</router-link>&nbsp;
                                    <button class="fs-16 btn btn-danger" @click="onDelete(autoPart._id)">Xóa</button>
                                </td>
                            </tr>
                        </template>
                        <template v-else>
                            <tr>
                                <td colspan="13" class="text-center">
                                    Bạn chưa có đồ uống nào.
                                    <router-link to="/admin/autoPart/create">Thêm đồ uống</router-link>
                                </td>
                            </tr>
                        </template>
                    </tbody>
                </table>
                <div class="admin-content__table-footer">
                    <router-link to="/admin/autoPart/trash">Thùng rác
                        <i class="fa-solid fa-trash admin-content__trash"></i>
                    </router-link>
                    <span class="header__notice admin-content__trash-notice">{{ deletedCount }}</span>
                </div>
            </div>
            <AdminPagination :totalPages="10" :currentPage="1"/>
        </div>
    </div>
</template>

<script>
import LineChart from '@/components/LineChart.vue';
import BarChart from '@/components/BarChart.vue';
import DoughnutChart from '@/components/DoughnutChart.vue';
import AdminPagination from '@/components/AdminPagination.vue';
import SortComponent from '@/components/SortComponent.vue';

export default {
    data() {
        return {
            autoParts: [
                {
                    name: "Lọc dầu động cơ",
                    category: "Lọc dầu",
                    supplier: "Nhà cung cấp A",
                    listPrice: 200000,
                    promotion: "10%",
                    quantity: 50,
                    unit: "Cái",
                    createdAt: "2024-01-10T12:00:00Z",
                    updatedAt: "2024-02-01T12:00:00Z",
                    status: "active"
                },
                {
                    name: "Bugi xe máy",
                    category: "Phụ kiện động cơ",
                    supplier: "Nhà cung cấp B",
                    listPrice: 150000,
                    promotion: "5%",
                    quantity: 30,
                    unit: "Bộ",
                    createdAt: "2023-12-15T12:00:00Z",
                    updatedAt: "2024-01-20T12:00:00Z",
                    status: "inactive"
                },
                {
                    name: "Má phanh xe hơi",
                    category: "Phanh & Hệ thống treo",
                    supplier: "Nhà cung cấp C",
                    listPrice: 500000,
                    promotion: "15%",
                    quantity: 20,
                    unit: "Cặp",
                    createdAt: "2023-11-05T12:00:00Z",
                    updatedAt: "2024-02-10T12:00:00Z",
                    status: "active"
                },
                {
                    name: "Đèn pha LED",
                    category: "Hệ thống chiếu sáng",
                    supplier: "Nhà cung cấp D",
                    listPrice: 750000,
                    promotion: "20%",
                    quantity: 15,
                    unit: "Bộ",
                    createdAt: "2023-10-20T12:00:00Z",
                    updatedAt: "2024-01-25T12:00:00Z",
                    status: "active"
                },
                {
                    name: "Cảm biến áp suất lốp",
                    category: "Cảm biến",
                    supplier: "Nhà cung cấp E",
                    listPrice: 1200000,
                    promotion: "25%",
                    quantity: 10,
                    unit: "Bộ",
                    createdAt: "2023-09-30T12:00:00Z",
                    updatedAt: "2024-02-05T12:00:00Z",
                    status: "active"
                },
                {
                    name: "Ắc quy xe hơi",
                    category: "Hệ thống điện",
                    supplier: "Nhà cung cấp F",
                    listPrice: 3000000,
                    promotion: "30%",
                    quantity: 5,
                    unit: "Cái",
                    createdAt: "2023-08-15T12:00:00Z",
                    updatedAt: "2024-01-10T12:00:00Z",
                    status: "inactive"
                },
                {
                    name: "Bộ lọc gió động cơ",
                    category: "Lọc dầu",
                    supplier: "Nhà cung cấp A",
                    listPrice: 180000,
                    promotion: "10%",
                    quantity: 40,
                    unit: "Cái",
                    createdAt: "2023-07-25T12:00:00Z",
                    updatedAt: "2024-02-01T12:00:00Z",
                    status: "active"
                },
                {
                    name: "Cảm biến lùi xe",
                    category: "Cảm biến",
                    supplier: "Nhà cung cấp E",
                    listPrice: 950000,
                    promotion: "25%",
                    quantity: 25,
                    unit: "Bộ",
                    createdAt: "2023-06-20T12:00:00Z",
                    updatedAt: "2024-02-08T12:00:00Z",
                    status: "inactive"
                },
                {
                    name: "Gạt nước mưa",
                    category: "Phụ kiện ngoại thất",
                    supplier: "Nhà cung cấp G",
                    listPrice: 350000,
                    promotion: "10%",
                    quantity: 60,
                    unit: "Cặp",
                    createdAt: "2023-05-15T12:00:00Z",
                    updatedAt: "2024-01-20T12:00:00Z",
                    status: "active"
                },
                {
                    name: "Bạt phủ ô tô",
                    category: "Bảo vệ xe",
                    supplier: "Nhà cung cấp H",
                    listPrice: 800000,
                    promotion: "15%",
                    quantity: 12,
                    unit: "Cái",
                    createdAt: "2023-04-10T12:00:00Z",
                    updatedAt: "2024-02-12T12:00:00Z",
                    status: "active"
                }
            ],
            sort: {},
            chartOptions: {
                responsive: true,
                maintainAspectRatio: false
            },
            lineData: {
                labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May'],
                datasets: [
                    {
                        label: 'Doanh thu',
                        data: [65, 59, 80, 81, 56],
                        borderColor: '#4CAF50',
                        tension: 0.1
                    }
                ]
            },
            barData: {
                labels: ['Sản phẩm A', 'Sản phẩm B', 'Sản phẩm C'],
                datasets: [
                    {
                        label: 'Bán hàng',
                        data: [12, 19, 3],
                        backgroundColor: ['#2196F3', '#4CAF50', '#FFC107']
                    }
                ]
            },
            doughnutData: {
                labels: ['Đỏ', 'Xanh', 'Vàng'],
                datasets: [
                    {
                        data: [300, 50, 100],
                        backgroundColor: ['#FF6384', '#36A2EB', '#FFCE56']
                    }
                ]
            }
        }
    },
    components: {
        LineChart, BarChart, DoughnutChart, 
        AdminPagination, SortComponent
    },
    methods: {

    },
}
</script>