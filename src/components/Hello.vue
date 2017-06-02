<template>
  <div class="hello">
        <div v-if="!dangnhap" class="bodyLogin">
            <form class="formLogin" @submit.prevent="funcdangnhap()">
              <!-- <el-input
                placeholder="Tài khoản"
                v-model="username" class="inputLogin"
                >
              </el-input>
              <el-input
                  placeholder="Mật khẩu"
                  v-model="password" class="inputLogin">
              </el-input> -->
                <input class="form-control" v-model="username" type="text" placeholder="Tài khoản">
                <input class="form-control" v-model="password" type="password" placeholder="Mật khẩu">
                <button type="submit" v-on:click="funcdangnhap()" class="btnLogin btn">ĐĂNG NHẬP</button>
                <label v-if="errr">{{messageerr}}</label>
            </form>
        </div>
    <div v-else>
    <el-row>
      <el-col :span="24">
        <el-col :xs="24" :sm="24" :md="24">
          <h1 class="titleMain">{{msg}}</h1>
        </el-col>
        <el-col :xs="24" :sm="24" :md="24">
          <el-button v-if="!checkadd" v-on:click="showadduser()" class="addbtn"type="primary"><i class="el-icon-edit"></i> Thêm thành viên</el-button>
          <el-button v-else v-on:click="doneadduser()" class="addbtn"type="primary"><i class="el-icon-close"></i> Đóng</el-button>
        </el-col>
      </el-col>
    </el-row>
    <el-row v-if="checkadd">
      <el-col :span="24">
        <div class="panel panel-default">
          <div class="panel-body bgForm">
            <h4 class="titleh4">Nhập thông tin thành viên mới</h4>
            <form class="form-inline" id="add" v-on:submit.prevent="addUser">
              <el-col :xs="24" :sm="12" :md="6">
                <div class="form-group">
                  <label for="GoiTap">Họ và tên</label>
                  <el-input class="fullform"
                    placeholder="Nguyễn Văn A..."
                    v-model="newuser.name">
                  </el-input>
                </div>
              </el-col>
              <el-col :sx="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="gioitinh">Giới tính</label>
                <el-select class="fullform" v-model="newuser.gioitinh" placeholder="Nam/Nữ">
                  <el-option
                    v-for="item in listgioitinh"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="lop">Lớp</label>
                <el-select class="fullform" v-model="newuser.goi" placeholder="Gym/Aerobic">
                  <el-option
                    v-for="item in listphongtap"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="lop">Gói tập</label>
                <el-input class="fullform"
                  placeholder=""
                  v-model="newuser.goitap">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Năm sinh</label>
                <el-input
                  placeholder="Nhập năm sinh"
                  icon="date"
                  v-model="newuser.birthday">
                </el-input>
                <!-- <input class="form-group" type="date" v-model="newuser.birthday"> -->
              </div>
            </el-col>
            <!-- <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Địa chỉ</label>
                <el-input class="fullform"
                  placeholder="Please Input"
                  v-model="newuser.diachi">
                </el-input>
              </div>
            </el-col> -->
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày phát hành</label>
                <input class="form-group el-input__inner" type="date" v-model="newuser.phathanhkoshow">
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày gia hạn</label>
                <input class="form-group el-input__inner" type="date" v-model="newuser.giahankoshow">
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Số tháng gia hạn thêm</label>
                <el-input class="fullform"
                  placeholder="1 tháng = 30 ngày"
                  v-model="newuser.sothang" min="1" type="number">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="24" :md="24">
            <el-button v-on:click="addUser"type="primary" class="mgn_left_10">Thêm</el-button>
            </el-col>
            </form>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row v-if="checkupdate">
      <el-col :span="24">
        <!-- <h1>Update user</h1> -->
        <div class="panel panel-default">
          <div class="panel-body bgForm2">
            <h4 class="titleh4">Chỉnh sửa thông tin thành viên</h4>
            <form class="form-inline" id="add" v-on:submit.prevent="addUser">
              <el-col :xs="24" :sm="12" :md="6">
                <div class="form-group">
                  <label for="GoiTap">Họ và tên</label>
                  <el-input class="fullform"
                    v-model="userupdate.name">
                  </el-input>
                </div>
              </el-col>
              <el-col :sx="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="gioitinh">Giới tính</label>
                <el-select class="fullform" v-model="userupdate.gioitinh" placeholder="Nam/Nữ">
                  <el-option
                    v-for="item in listgioitinh"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="lop">Lớp</label>
                <el-select class="fullform" v-model="userupdate.goi" placeholder="Select">
                  <el-option
                    v-for="item in listphongtap"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="lop">Gói tập</label>
                <el-input class="fullform"
                  placeholder=""
                  v-model="userupdate.goitap">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Năm sinh</label>
                <el-input
                  placeholder="Nhập năm sinh"
                  icon="date"
                  v-model="userupdate.birthday">
                </el-input>
              </div>
            </el-col>
            <!-- <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Địa chỉ</label>
                <el-input class="fullform"
                  placeholder="Please Input"
                  v-model="userupdate.diachi">
                </el-input>
              </div>
            </el-col> -->
            <!-- <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày phát hành</label>
                <input class="form-group el-input__inner" type="date" v-model="userupdate.phathanhkoshow">
              </div>
            </el-col> -->
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày gia hạn</label>
                <input class="form-group el-input__inner" type="date" v-model="userupdate.giahankoshow">
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Số tháng gia hạn</label>
                <el-input class="fullform"
                  placeholder="1 tháng = 30 ngày"
                  v-model="userupdate.sothang" min="1" type="number">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="24" :md="24">
            <el-button v-on:click="updateUser" type="primary" class="mgn_left_10" icon="check">Cập nhật</el-button>
            <el-button v-on:click="closeupdate" type="primary" class="btn-red" icon="close">Đóng</el-button>
            </el-col>
            </form>
          </div>
        </div>
      </el-col>
    </el-row>

    <!-- <div class="page-header">
      <h1>{{msg}}</h1>
    </div> -->
    <div class="panel panel-default">
      <div class="panel-heading">
        <h3 class="titleSearchMem"><i class="el-icon-search"></i> Tìm thành viên</h3>
        <form class="group-inline" id="search" v-cloak>
          <div class="form-group searchMember ">
            <input type="text" class="el-input__inner" v-model="searchString" placeholder="Nhập tên cần tìm">
          </div>
        </form>
      </div>
      <div class="panel-body">
        <h3 class="titleAll">Danh sách tất cả thành viên</h3>
        <table class="table table-striped">
          <thead>
            <tr>
              <th>STT</th>
              <!-- <th>Mã KH</th> -->
              <th class="tal">Lớp</th>
              <th class="tal">Gói tập</th>
              <th class="tal">Họ và tên</th>
              <th>Năm sinh</th>
              <th class="tal">Giới tính</th>
              <!-- <th>Địa chỉ</th> -->
              <th>Ngày phát hành</th>
              <th>Ngày gia hạn</th>
              <th>Số tháng đóng</th>
              <th>Ngày hết hạn</th>
              <th>Trạng thái</th>
              <th>Cập nhật</th>
              <th>Ẩn</th>
            </tr>
          </thead>
            <transition-group name="fade" tag="tbody">
            <tr class="user" v-if="!user.checked" v-for="user in filterUser" v-bind:key="user" >
              <!-- <td class="tac">{{user.stt}}</td> -->
              <td><!-- dành cho stt --></td>
              <!-- <td>{{user.makh}}</td> -->
              <td class="tal">{{user.goi}}</td>
              <td class="tal">{{user.goitap}}</td>
              <td class="tal">{{user.name}}</td>
              <td>{{user.birthday}}</td>
              <td class="tal">{{user.gioitinh}}</td>
              <!-- <td>{{user.diachi}}</td> -->
              <td>{{user.phathanh}}</td>
              <td>{{user.giahan}}</td>
              <td>{{user.sothang}}</td>
              <td>{{user.hethan}}</td>
              <td>{{user.trangthai}}</td>
              <td class="tac btnEdit"><span class="el-icon-edit updatefun" v-on:click="update(user)" title="Chỉnh sửa"></span>
              </td>
              <td v-if="user.checkhethan"><label class="switch" >
              <input v-on:click="check(user)" type="checkbox" id="checkbox" v-model="user.checked" checked>
              <div class="slider round"></div>
              </label></td>
              <td v-else></td>
            </tr>
          </transition-group>
        </table>
        <div class="listHethan">
            <h3 class="titleHethan">Danh sách thành viên đã hết hạn</h3>
            <table class="table table-striped">
                <thead>
                    <tr>
                        <th>STT</th>
                        <th class="tal">Lớp</th>
                        <th class="tal">Gói tập</th>
                        <th class="tal">Họ và tên</th>
                        <th>Năm sinh</th>
                        <th class="tal">Giới tính</th>
                        <th>Ngày phát hành</th>
                        <th>Ngày gia hạn</th>
                        <th>Số tháng đóng</th>
                        <th>Ngày hết hạn</th>
                        <th>Trạng thái</th>
                        <th>Cập nhật</th>
                        <th>Ẩn</th>
                    </tr>
                </thead>
                  <transition-group name="fade" tag="tbody">
                    <tr v-if="!userhh.checked" v-for="userhh in filterUserhethan"  v-bind:key="userhh">
                        <td><!--STT--></td>
                        <td class="tal">{{userhh.goi}}</td>
                        <td class="tal">{{userhh.goitap}}</td>
                        <td class="tal">{{userhh.name}}</td>
                        <td>{{userhh.birthday}}</td>
                        <td>{{userhh.gioitinh}}</td>
                        <td>{{userhh.phathanh}}</td>
                        <td>{{userhh.giahan}}</td>
                        <td>{{userhh.sothang}}</td>
                        <td>{{userhh.hethan}}</td>
                        <td>{{userhh.trangthai}}</td>
                        <td class="tac btnEdit"><span class="el-icon-edit updatefun" v-on:click="update(userhh)" title="Chỉnh sửa"></span>
                        </td>
                        <td><label class="switch" >
                        <input v-on:click="check(userhh)" type="checkbox" id="checkbox" v-model="userhh.checked" checked>
                        <div class="slider round"></div>
                        </label></td>
                    </tr>
                </transition-group>
            </table>
        </div>
        <div class="listHide">
            <h3 class="titleHide">Danh sách thành viên bị ẩn</h3>
            <p class="red_italic">(thành viên đã nghỉ tập lâu ngày không gia hạn)</p>
            <table class="table table-hover table-striped">
                <thead>
                    <tr>
                        <th>STT</th>
                        <th class="tal">Lớp</th>
                        <th class="tal">Gói tập</th>
                        <th class="tal">Họ và tên</th>
                        <th>Năm sinh</th>
                        <th class="tal">Giới tính</th>
                        <th>Ngày phát hành</th>
                        <th>Ngày gia hạn</th>
                        <th>Số tháng đóng</th>
                        <th>Ngày hết hạn</th>
                        <th>Trạng thái</th>
                        <th>Cập nhật</th>
                        <th>Ẩn</th>
                        <th>Xoá</th>
                    </tr>
                </thead>
                  <transition-group name="fade" tag="tbody">
                    <tr v-for="userhh in filtercheckan"  v-bind:key="userhh">
                      <td><!--STT--></td>
                      <td class="tal">{{userhh.goi}}</td>
                      <td class="tal">{{userhh.goitap}}</td>
                      <td class="tal">{{userhh.name}}</td>
                      <td>{{userhh.birthday}}</td>
                      <td>{{userhh.gioitinh}}</td>
                      <td>{{userhh.phathanh}}</td>
                      <td>{{userhh.giahan}}</td>
                      <td>{{userhh.sothang}}</td>
                      <td>{{userhh.hethan}}</td>
                      <td>{{userhh.trangthai}}</td>
                      <td class="tac btnEdit"><span class="el-icon-edit updatefun" v-on:click="update(userhh)" title="Chỉnh sửa"></span>
                      </td>
                      <td><label class="switch" >
                      <input v-on:click="uncheck(userhh)" type="checkbox" id="checkbox" v-model="userhh.checked" checked>
                      <div class="slider round"></div>
                      </label></td>
                      <td><span class="el-icon-delete updatefun red" v-on:click="xoauser(userhh)" title="Xóa"></span></td>
                    </tr>
                </transition-group>
            </table>
        </div>
      </div>
    </div>
    <footer class="footer">
        <h4>Hệ thống phòng tập <span class="blue">Gym và Aerobic Olympia</span>: 150 Đoàn Hữu Trưng, Hòa An, Cẩm Lệ, Đà Nẵng</h4>
    </footer>
  </div>
    <simplert useRadius=true
              useIcon=true
              ref="simplert">
      </simplert>
  </div>

</template>

<script>
import Firebase from 'Firebase'
import moment from 'moment'

let config = {
  apiKey: 'AIzaSyDg4PMF2hQ6ZtjywC1ZDzM9J0i-igqo-tI',
  authDomain: 'phongtap-95ebd.firebaseapp.com',
  databaseURL: 'https://phongtap-95ebd.firebaseio.com',
  projectId: 'phongtap-95ebd',
  storageBucket: 'phongtap-95ebd.appspot.com',
  messagingSenderId: '225931463676'
}
let app = Firebase.initializeApp(config)
let db = app.database()
let danhsachref = db.ref('danhsach')
let admin = db.ref('admin')
export default {
  name: 'hello',
  components: {
    'vue-datetime-picker': require('vue-datetime-picker'),
    'Simplert': require('vue2-simplert')
  },
  firebase: {
    listuser: danhsachref,
    usernamedn: admin
  },
  data () {
    return {
      msg: 'HỆ THỐNG QUẢN LÝ THÀNH VIÊN',
      listgioitinh: [{
        value: 'Nam',
        label: 'Nam'
      },
      {
        value: 'Nữ',
        label: 'Nữ'
      }],
      listphongtap: [
        {
          value: 'Gym',
          label: 'Gym'
        },
        {
          value: 'Aerobic',
          label: 'Aerobic'
        }
      ],
      newuser: {
        stt: '',
        goi: '',
        lop: '',
        name: '',
        'birthday': '',
        gioitinh: '',
        diachi: '',
        phathanh: '',
        phathanhkoshow: '',
        sothang: '',
        giahan: '',
        goitap: '',
        giahankoshow: '',
        hethan: '',
        hethankoshow: '',
        checkhethan: false,
        trangthai: '',
        key: '',
        checked: false
      },
      searchString: '',
      stt: '',
      makh: '',
      goi: '',
      lop: '',
      name: '',
      birthday: '',
      gioitinh: '',
      diachi: '',
      phathanh: '',
      sothang: '',
      giahan: '',
      hethan: '',
      trangthai: '',
      checkadd: false,
      checkupdate: false,
      checked: false,
      userupdate: '',
      userupdate2: '',
      key1: '',
      key2: '',
      dangnhap: false,
      username: '',
      password: '',
      messageerr: '',
      errr: false
    }
  },
  computed: {
    filterUser: function () {
      var ngayhientai = moment().date()
      var thanghientai = moment().month() + 1
      var namhientai = moment().year()
      console.log(this.usernamedn)
      var articlearray = this.listuser.map(function (item) {
        console.log('=>>')
        if (namhientai > moment(item.hethankoshow).year()) {
          item.trangthai = 'Đã hết hạn'
        } else if (namhientai === moment(item.hethankoshow).year()) {
          if (thanghientai > moment(item.hethankoshow).month() + 1) {
            item.trangthai = 'Đã hết hạn'
          } else if (thanghientai === moment(item.hethankoshow).month() + 1) {
            if (ngayhientai >= moment(item.hethankoshow).date()) {
              item.trangthai = 'Đã hết hạn'
            } else {
              item.trangthai = 'Chưa hết hạn'
            }
          } else {
            item.trangthai = 'Chưa hết hạn'
          }
        } else {
          item.trangthai = 'Chưa hết hạn'
        }
        return item
      })
      var searchitem = this.searchString
      // console.log(articlearray)
      if (!searchitem) {
        return articlearray
      }
      searchitem = searchitem.trim().toLowerCase()

      articlearray = articlearray.filter(function (item) {
        if (item.name.toLowerCase().indexOf(searchitem) !== -1) {
          return item
        }
      })
      return articlearray
    },
    filterUserhethan: function () {
      var arrayuser = this.listuser.filter(function (item) {
        if (item.checkhethan === true) {
          return item
        }
      })
      return arrayuser
    },
    filtercheckan: function () {
      var arrayuser = this.listuser.filter(function (item) {
        if (item.checked === true) {
          return item
        }
      })
      return arrayuser
    }
  },
  methods: {
    addUser: function () {
      var dategiahan = moment(this.newuser.giahankoshow)
      // var parts = dategiahan.match(/(\d+)/g)
      // var dateafterconvert = new Date(parts[0], parts[1] - 1, parts[2])
      var x = moment(dategiahan).format('DD/MM/YYYY')
      var y = moment(dategiahan).format('L')
      var datephathanh = moment(this.newuser.phathanhkoshow)
      var xph = moment(datephathanh).format('DD/MM/YYYY')
      this.newuser.giahankoshow = moment(dategiahan).format('L')
      this.newuser.phathanhkoshow = moment(datephathanh).format('L')
      this.newuser.phathanh = xph
      this.newuser.giahan = x
      var getdate = moment(y).add(30 * this.newuser.sothang, 'days')
      var datehethan = moment(getdate).format('DD/MM/YYYY')
      this.newuser.hethan = datehethan
      this.newuser.hethankoshow = moment(getdate).format('L')
      this.newuser.stt = this.listuser.length + 1
      var ngayhientai = moment().date()
      var thanghientai = moment().month() + 1
      var namhientai = moment().year()
      if (namhientai > moment(this.newuser.hethankoshow).year()) {
        this.newuser.checkhethan = true
      } else if (namhientai === moment(this.newuser.hethankoshow).year()) {
        if (thanghientai > moment(this.newuser.hethankoshow).month() + 1) {
          this.newuser.checkhethan = true
        } else if (thanghientai === moment(this.newuser.hethankoshow).month() + 1) {
          if (ngayhientai >= moment(this.newuser.hethankoshow).date()) {
            this.newuser.checkhethan = true
          } else {
            this.newuser.checkhethan = false
          }
        } else {
          this.newuser.checkhethan = false
        }
      } else {
        this.newuser.checkhethan = false
      }
      // if ((ngayhientai >= moment(this.newuser.hethankoshow).date()) && (thanghientai >= moment(this.newuser.hethankoshow).month() + 1) && (namhientai >= moment(this.newuser.hethankoshow).year())) {
      //   console.log('het han')
      //   this.newuser.checkhethan = true
      // } else {
      //   console.log('chua het han')
      //   this.newuser.checkhethan = false
      // }
      danhsachref.push(this.newuser)
      this.newuser.stt = ''
      this.newuser.goi = ''
      this.newuser.lop = ''
      this.newuser.name = ''
      this.newuser.birthday = ''
      this.newuser.gioitinh = ''
      this.newuser.diachi = ''
      this.newuser.phathanh = ''
      this.newuser.sothang = ''
      this.newuser.giahan = ''
      this.newuser.hethan = ''
      this.newuser.trangthai = ''
    },
    updateUser: function () {
      var dategiahan = moment(this.userupdate.giahankoshow)
      var x = moment(dategiahan).format('L')
      var y = moment(dategiahan).format('DD/MM/YYYY')
      var datephathanh = moment(this.userupdate.phathanhkoshow)
      var xph = moment(datephathanh).format('DD/MM/YYYY')
      this.userupdate.giahankoshow = moment(dategiahan).format('L')
      this.userupdate.phathanhkoshow = moment(datephathanh).format('L')
      this.userupdate.phathanh = xph
      var getdate = moment(x).add(30 * this.userupdate.sothang, 'days')
      var datehethan = moment(getdate).format('DD/MM/YYYY')
      this.userupdate.hethan = datehethan
      this.userupdate.hethankoshow = moment(getdate).format('L')
      this.userupdate.giahan = y
      if (this.userupdate.key === '') {
        this.userupdate.key = this.key1
      }
      var ngayhientai = moment().date()
      var thanghientai = moment().month() + 1
      var namhientai = moment().year()
      if (namhientai > moment(this.userupdate.hethankoshow).year()) {
        this.userupdate.checkhethan = true
      } else if (namhientai === moment(this.userupdate.hethankoshow).year()) {
        if (thanghientai > moment(this.userupdate.hethankoshow).month() + 1) {
          this.userupdate.checkhethan = true
        } else if (thanghientai === moment(this.userupdate.hethankoshow).month() + 1) {
          if (ngayhientai >= moment(this.userupdate.hethankoshow).date()) {
            this.userupdate.checkhethan = true
          } else {
            this.userupdate.checkhethan = false
          }
        } else {
          this.userupdate.checkhethan = false
        }
      } else {
        this.userupdate.checkhethan = false
      }
      // if ((ngayhientai >= moment(this.userupdate.hethankoshow).date()) && (thanghientai >= moment(this.userupdate.hethankoshow).month() + 1) && (namhientai >= moment(this.userupdate.hethankoshow).year())) {
      //   console.log('het han')
      //   this.userupdate.checkhethan = true
      // } else {
      //   console.log('chua het han')
      //   this.userupdate.checkhethan = false
      // }
      this.hamupdate(this.userupdate, this.userupdate.birthday, 'birthday')
      this.hamupdate(this.userupdate, this.userupdate.checked, 'checked')
      this.hamupdate(this.userupdate, this.userupdate.checkhethan, 'checkhethan')
      this.hamupdate(this.userupdate, this.userupdate.diachi, 'diachi')
      this.hamupdate(this.userupdate, this.userupdate.giahan, 'giahan')
      this.hamupdate(this.userupdate, this.userupdate.giahankoshow, 'giahankoshow')
      this.hamupdate(this.userupdate, this.userupdate.gioitinh, 'gioitinh')
      this.hamupdate(this.userupdate, this.userupdate.goi, 'goi')
      this.hamupdate(this.userupdate, this.userupdate.goitap, 'goitap')
      this.hamupdate(this.userupdate, this.userupdate.hethan, 'hethan')
      this.hamupdate(this.userupdate, this.userupdate.hethankoshow, 'hethankoshow')
      this.hamupdate(this.userupdate, this.userupdate.key, 'key')
      this.hamupdate(this.userupdate, this.userupdate.lop, 'lop')
      this.hamupdate(this.userupdate, this.userupdate.name, 'name')
      this.hamupdate(this.userupdate, this.userupdate.phathanh, 'phathanh')
      this.hamupdate(this.userupdate, this.userupdate.phathanhkoshow, 'phathanhkoshow')
      this.hamupdate(this.userupdate, this.userupdate.sothang, 'sothang')
      this.hamupdate(this.userupdate, this.userupdate.stt, 'stt')
      this.hamupdate(this.userupdate, this.userupdate.trangthai, 'trangthai')
      this.checkupdate = false
      // let key = this.userupdate['.key']
      // delete this.userupdate['.key']
      // console.log(this.userupdate)
      // console.log(key)
      // danhsachref.child(key).set(this.userupdate)
      // console.log(this.listuser)
      // this.userupdate = ''
      // console.log(this.userupdate)
      // this.filterUser
    },
    closeupdate: function () {
      this.checkupdate = false
    },
    showadduser: function () {
      this.checkadd = true
    },
    doneadduser: function () {
      this.checkadd = false
    },
    update: function (user) {
      window.scrollTo(0, 0)
      this.userupdate2 = user
      this.userupdate = this.userupdate2
      this.key1 = user['.key']
      if (this.key1 != null) {
        this.key2 = this.key1
      }
      this.checkupdate = true
    },
    check: function (user) {
      // var key = user['.key']
      // delete user['.key']
      // danhsachref.child(key).set(user)
      this.hamupdate(user, user.checked, 'checked')
      // console.log('check')
      // console.log(user.checked)
    },
    hamupdate: function (user, value, truong) {
      danhsachref.child(user['.key']).child(truong).set(value)
    },
    funcdangnhap: function () {
      var ps = this.md5(this.password)
      if (this.username === this.usernamedn[0].username && ps === this.usernamedn[0].password) {
        this.errr = false
        this.messageerr = ''
        this.dangnhap = true
      } else {
        this.errr = true
        this.messageerr = 'Sai tài khoản hoặc mật khẩu'
      }
    },
    uncheck: function (user) {
      this.hamupdate(user, user.checked, 'checked')
      // var key = user['.key']
      // delete user['.key']
      // danhsachref.child(key).set(user)
      // console.log('check')
      // console.log(user.checked)
    },
    xoauser: function (user) {
      danhsachref.child(user['.key']).remove()
    },
    md5: function (string) {
      function RotateLeft (lValue, iShiftBits) {
        return (lValue << iShiftBits) | (lValue >>> (32 - iShiftBits))
      }
      function AddUnsigned (lX, lY) {
        var lX4, lY4, lX8, lY8, lResult
        lX8 = (lX & 0x80000000)
        lY8 = (lY & 0x80000000)
        lX4 = (lX & 0x40000000)
        lY4 = (lY & 0x40000000)
        lResult = (lX & 0x3FFFFFFF) + (lY & 0x3FFFFFFF)
        if (lX4 & lY4) {
          return (lResult ^ 0x80000000 ^ lX8 ^ lY8)
        }
        if (lX4 | lY4) {
          if (lResult & 0x40000000) {
            return (lResult ^ 0xC0000000 ^ lX8 ^ lY8)
          } else {
            return (lResult ^ 0x40000000 ^ lX8 ^ lY8)
          }
        } else {
          return (lResult ^ lX8 ^ lY8)
        }
      }
      function F (x, y, z) {
        return (x & y) | ((~x) & z)
      }
      function G (x, y, z) {
        return (x & z) | (y & (~z))
      }
      function H (x, y, z) {
        return (x ^ y ^ z)
      }
      function I (x, y, z) {
        return (y ^ (x | (~z)))
      }
      function FF (a, b, c, d, x, s, ac) {
        a = AddUnsigned(a, AddUnsigned(AddUnsigned(F(b, c, d), x), ac))
        return AddUnsigned(RotateLeft(a, s), b)
      }

      function GG (a, b, c, d, x, s, ac) {
        a = AddUnsigned(a, AddUnsigned(AddUnsigned(G(b, c, d), x), ac))
        return AddUnsigned(RotateLeft(a, s), b)
      }
      function HH (a, b, c, d, x, s, ac) {
        a = AddUnsigned(a, AddUnsigned(AddUnsigned(H(b, c, d), x), ac))
        return AddUnsigned(RotateLeft(a, s), b)
      }
      function II (a, b, c, d, x, s, ac) {
        a = AddUnsigned(a, AddUnsigned(AddUnsigned(I(b, c, d), x), ac))
        return AddUnsigned(RotateLeft(a, s), b)
      }
      function ConvertToWordArray (string) {
        var lWordCount
        var lMessageLength = string.length
        var lNumberOfWordstemp1 = lMessageLength + 8
        var lNumberOfWordstemp2 = (lNumberOfWordstemp1 - (lNumberOfWordstemp1 % 64)) / 64
        var lNumberOfWords = (lNumberOfWordstemp2 + 1) * 16
        var lWordArray = Array(lNumberOfWords - 1)
        var lBytePosition = 0
        var lByteCount = 0
        while (lByteCount < lMessageLength) {
          lWordCount = (lByteCount - (lByteCount % 4)) / 4
          lBytePosition = (lByteCount % 4) * 8
          lWordArray[lWordCount] = (lWordArray[lWordCount] | (string.charCodeAt(lByteCount) << lBytePosition))
          lByteCount++
        }
        lWordCount = (lByteCount - (lByteCount % 4)) / 4
        lBytePosition = (lByteCount % 4) * 8
        lWordArray[lWordCount] = lWordArray[lWordCount] | (0x80 << lBytePosition)
        lWordArray[lNumberOfWords - 2] = lMessageLength << 3
        lWordArray[lNumberOfWords - 1] = lMessageLength >>> 29
        return lWordArray
      }
      function WordToHex (lValue) {
        var WordToHexValue = ''
        var WordToHexValuetemp = ''
        var lByte
        var lCount
        for (lCount = 0; lCount <= 3; lCount++) {
          lByte = (lValue >>> (lCount * 8)) & 255
          WordToHexValuetemp = '0' + lByte.toString(16)
          WordToHexValue = WordToHexValue + WordToHexValuetemp.substr(WordToHexValuetemp.length - 2, 2)
        }
        return WordToHexValue
      }
      function Utf8Encode (string) {
        string = string.replace(/\r\n/g, '\n')
        var utftext = ''
        for (var n = 0; n < string.length; n++) {
          var c = string.charCodeAt(n)
          if (c < 128) {
            utftext += String.fromCharCode(c)
          } else if ((c > 127) && (c < 2048)) {
            utftext += String.fromCharCode((c >> 6) | 192)
            utftext += String.fromCharCode((c & 63) | 128)
          } else {
            utftext += String.fromCharCode((c >> 12) | 224)
            utftext += String.fromCharCode(((c >> 6) & 63) | 128)
            utftext += String.fromCharCode((c & 63) | 128)
          }
        }
        return utftext
      }
      var x = []
      var k, AA, BB, CC, DD, a, b, c, d
      var S11 = 7
      var S12 = 12
      var S13 = 17
      var S14 = 22
      var S21 = 5
      var S22 = 9
      var S23 = 14
      var S24 = 20
      var S31 = 4
      var S32 = 11
      var S33 = 16
      var S34 = 23
      var S41 = 6
      var S42 = 10
      var S43 = 15
      var S44 = 21
      string = Utf8Encode(string)
      x = ConvertToWordArray(string)
      a = 0x67452301
      b = 0xEFCDAB89
      c = 0x98BADCFE
      d = 0x10325476
      for (k = 0; k < x.length; k += 16) {
        AA = a
        BB = b
        CC = c
        DD = d
        a = FF(a, b, c, d, x[k + 0], S11, 0xD76AA478)
        d = FF(d, a, b, c, x[k + 1], S12, 0xE8C7B756)
        c = FF(c, d, a, b, x[k + 2], S13, 0x242070DB)
        b = FF(b, c, d, a, x[k + 3], S14, 0xC1BDCEEE)
        a = FF(a, b, c, d, x[k + 4], S11, 0xF57C0FAF)
        d = FF(d, a, b, c, x[k + 5], S12, 0x4787C62A)
        c = FF(c, d, a, b, x[k + 6], S13, 0xA8304613)
        b = FF(b, c, d, a, x[k + 7], S14, 0xFD469501)
        a = FF(a, b, c, d, x[k + 8], S11, 0x698098D8)
        d = FF(d, a, b, c, x[k + 9], S12, 0x8B44F7AF)
        c = FF(c, d, a, b, x[k + 10], S13, 0xFFFF5BB1)
        b = FF(b, c, d, a, x[k + 11], S14, 0x895CD7BE)
        a = FF(a, b, c, d, x[k + 12], S11, 0x6B901122)
        d = FF(d, a, b, c, x[k + 13], S12, 0xFD987193)
        c = FF(c, d, a, b, x[k + 14], S13, 0xA679438E)
        b = FF(b, c, d, a, x[k + 15], S14, 0x49B40821)
        a = GG(a, b, c, d, x[k + 1], S21, 0xF61E2562)
        d = GG(d, a, b, c, x[k + 6], S22, 0xC040B340)
        c = GG(c, d, a, b, x[k + 11], S23, 0x265E5A51)
        b = GG(b, c, d, a, x[k + 0], S24, 0xE9B6C7AA)
        a = GG(a, b, c, d, x[k + 5], S21, 0xD62F105D)
        d = GG(d, a, b, c, x[k + 10], S22, 0x2441453)
        c = GG(c, d, a, b, x[k + 15], S23, 0xD8A1E681)
        b = GG(b, c, d, a, x[k + 4], S24, 0xE7D3FBC8)
        a = GG(a, b, c, d, x[k + 9], S21, 0x21E1CDE6)
        d = GG(d, a, b, c, x[k + 14], S22, 0xC33707D6)
        c = GG(c, d, a, b, x[k + 3], S23, 0xF4D50D87)
        b = GG(b, c, d, a, x[k + 8], S24, 0x455A14ED)
        a = GG(a, b, c, d, x[k + 13], S21, 0xA9E3E905)
        d = GG(d, a, b, c, x[k + 2], S22, 0xFCEFA3F8)
        c = GG(c, d, a, b, x[k + 7], S23, 0x676F02D9)
        b = GG(b, c, d, a, x[k + 12], S24, 0x8D2A4C8A)
        a = HH(a, b, c, d, x[k + 5], S31, 0xFFFA3942)
        d = HH(d, a, b, c, x[k + 8], S32, 0x8771F681)
        c = HH(c, d, a, b, x[k + 11], S33, 0x6D9D6122)
        b = HH(b, c, d, a, x[k + 14], S34, 0xFDE5380C)
        a = HH(a, b, c, d, x[k + 1], S31, 0xA4BEEA44)
        d = HH(d, a, b, c, x[k + 4], S32, 0x4BDECFA9)
        c = HH(c, d, a, b, x[k + 7], S33, 0xF6BB4B60)
        b = HH(b, c, d, a, x[k + 10], S34, 0xBEBFBC70)
        a = HH(a, b, c, d, x[k + 13], S31, 0x289B7EC6)
        d = HH(d, a, b, c, x[k + 0], S32, 0xEAA127FA)
        c = HH(c, d, a, b, x[k + 3], S33, 0xD4EF3085)
        b = HH(b, c, d, a, x[k + 6], S34, 0x4881D05)
        a = HH(a, b, c, d, x[k + 9], S31, 0xD9D4D039)
        d = HH(d, a, b, c, x[k + 12], S32, 0xE6DB99E5)
        c = HH(c, d, a, b, x[k + 15], S33, 0x1FA27CF8)
        b = HH(b, c, d, a, x[k + 2], S34, 0xC4AC5665)
        a = II(a, b, c, d, x[k + 0], S41, 0xF4292244)
        d = II(d, a, b, c, x[k + 7], S42, 0x432AFF97)
        c = II(c, d, a, b, x[k + 14], S43, 0xAB9423A7)
        b = II(b, c, d, a, x[k + 5], S44, 0xFC93A039)
        a = II(a, b, c, d, x[k + 12], S41, 0x655B59C3)
        d = II(d, a, b, c, x[k + 3], S42, 0x8F0CCC92)
        c = II(c, d, a, b, x[k + 10], S43, 0xFFEFF47D)
        b = II(b, c, d, a, x[k + 1], S44, 0x85845DD1)
        a = II(a, b, c, d, x[k + 8], S41, 0x6FA87E4F)
        d = II(d, a, b, c, x[k + 15], S42, 0xFE2CE6E0)
        c = II(c, d, a, b, x[k + 6], S43, 0xA3014314)
        b = II(b, c, d, a, x[k + 13], S44, 0x4E0811A1)
        a = II(a, b, c, d, x[k + 4], S41, 0xF7537E82)
        d = II(d, a, b, c, x[k + 11], S42, 0xBD3AF235)
        c = II(c, d, a, b, x[k + 2], S43, 0x2AD7D2BB)
        b = II(b, c, d, a, x[k + 9], S44, 0xEB86D391)
        a = AddUnsigned(a, AA)
        b = AddUnsigned(b, BB)
        c = AddUnsigned(c, CC)
        d = AddUnsigned(d, DD)
      }
      var temp = WordToHex(a) + WordToHex(b) + WordToHex(c) + WordToHex(d)
      return temp.toLowerCase()
    }
  }
}

</script>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

.bodyLogin {
    background: url('../assets/background.jpg')center no-repeat;
    background-color: #000;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: -1;
}
.formLogin {
    background: url('../assets/bg-form2.png');
    margin: auto;
    width: 600px;
    padding: 50px;
    position: absolute;
    left: 50%;
    top: 50%;
    -webkit-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
}
.formLogin .el-input {
    display: block;
    margin: 10px auto;
    border-radius: 0;
}
.formLogin label {
    color: red;
}
.formLogin input {
    height: 50px;
    margin: 5px 0;
    border-radius: 0;
}
.formLogin input:focus {
    box-shadow: none;
    border: 1px solid #2196F3;
}
.formLogin .btnLogin {
    background: #2196F3;
    color: #fff;
    height: 50px;
    width: 100%;
    border-radius: 0;
}
.panel-heading {
    border-bottom: 1px solid #2196F3;
}
.titleMain {
    position: relative;
    text-align: center;
    color: #fff;
    text-shadow: 0 0 10px rgba(0, 0, 0, 0.9);
}
.titleMain:after {
    content: "";
    position: absolute;
    bottom: -10px;
    left: 40%;
    width: 20%;
    height: 3px;
    background: #2196F3;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}
.titleSearchMem {
    color: #2196F3;
}
.titleh4 {
    color: red;
    text-align: center;
}
.fullform {
  width: 100%;
}
.form-group {
  width:100%;
  padding: 10px;
}
.addbtn {
  /*width:50px;*/
  /*height:50px;*/
  border-radius: 5px;
  float: right;
  margin: 20px;
}

/*--------------------
        Table area
        --------------------*/
table {
    border: 1px solid #E8E8E8;
    margin-bottom: 0;
}
table thead {
    background: #2196F3;
    color: #fff;
}
table thead th {
    text-align: center;
    /*font-weight: normal;*/
    font-size: 16px;
    padding: 12px 8px;
}
table tbody {
  counter-reset: rowNumber;
}
table tr {
  counter-increment: rowNumber;
}
table tr td:first-child::before {
  content: counter(rowNumber);
  min-width: 1em;
  margin-right: 0.5em;
}
table tr td{
    text-align: center;
    vertical-align: middle;
}

table tbody tr:hover {
    background: #D5ECFF;
    transition-duration: 500ms;
}
.titleAll {
    text-align: center;
    color: #2196F3;
}

.listHethan {
    padding: 20px 0;
}
.listHethan .titleHethan {
    color: #833200;
    text-align: center;
}
.listHethan table thead {
    background: #FFD24B;
}
.listHethan table thead th{
    color: #333;
}
.listHethan table tbody td {
    background: #FFFF86;
}
.listHethan table tbody tr:hover td{
    background: #FBF9E1;
    transition-duration: 500ms;
}
.listHide table thead {
    background: #0E3F52;
}
.listHide .titleHide {
    color: #0E3F52;
    text-align: center;
}
.red_italic {
    text-align: center;
    color: #ff0000;
    font-style: italic;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #2196F3;
}
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}
.switch input {display:none;}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}
input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}
.btnEdit span:hover{
    color: #2196F3;
}
.searchMember input {
    text-indent: 5px;
}
#search .form-group {
    padding: 0;
}
.user {
  transition: 1s;
}
/*--------------------
        Rounded sliders
        --------------------*/
.slider.round {
  border-radius: 34px;
}
.slider.round:before {
  border-radius: 50%;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0
}
.updatefun {
    color: #00508F;
    cursor: pointer;
    font-size: 25px;
}
.footer {
    text-align: center;
    color: #fff;
}
input {
    color: #0070C8;
}
.el-input__inner {
    color: #0070C8;
}
/*--------------------
        helper
        --------------------*/
.blue {
    color: #32A1F9;
}
.red {
    color: #E00000;
}
.btn-red {
    background: #E00000;
    border: 1px solid #E00000;
}
.tac {
    text-align: center;
}
.tal {
    text-align: left;
}
.mgn_left_10 {
    margin-left: 10px;
}
</style>
