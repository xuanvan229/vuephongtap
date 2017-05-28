<template>
  <div class="hello">

    <h2>{{checked}}</h2>
    <el-row>
      <el-col :span="24">
        <el-col :xs="12" :sm="12" :md="12">
          <h1>{{msg}}</h1>
        </el-col>
        <el-col :xs="12" :sm="12" :md="12">
          <el-button v-if="!checkadd" v-on:click="showadduser()"class="addbtn"type="primary"><i class="el-icon-edit"></i></el-button>
          <el-button v-else v-on:click="doneadduser()"class="addbtn"type="primary"><i class="el-icon-check"></i></el-button>
        </el-col>
      </el-col>
    </el-row>
    <el-row v-if="checkadd">
      <el-col :span="24">
        <div class="panel panel-default">
          <div class="panel-body">
            <form class="form-inline" id="add" v-on:submit.prevent="addUser">
              <el-col :sx="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="gioitinh">Giới Tính</label>
                <el-select class="fullform" v-model="newuser.gioitinh" placeholder="Select">
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
                <el-select class="fullform" v-model="newuser.goi" placeholder="Select">
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
                <label for="GoiTap">Họ và Tên</label>
                <el-input class="fullform"
                  placeholder="Please Input"
                  v-model="newuser.name">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày sinh</label>
                <el-input
                  placeholder="Pick a date"
                  icon="search"
                  v-model="newuser.birthday">
                </el-input>
                <!-- <input class="form-group" type="date" v-model="newuser.birthday"> -->
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Địa chỉ</label>
                <el-input class="fullform"
                  placeholder="Please Input"
                  v-model="newuser.diachi">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày phát hành</label>
                <input class="form-group" type="date" v-model="newuser.phathanh">
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày gia hạn</label>
                <input class="form-group" type="date" v-model="newuser.giahan">
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Số tháng đóng</label>
                <el-input class="fullform"
                  placeholder="Please Input"
                  v-model="newuser.sothang">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="24" :md="24">
            <el-button v-on:click="addUser"type="primary">Primary Button</el-button>
            </el-col>
            </form>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row v-if="checkupdate">
      <el-col :span="24">
        <h1>Update user</h1>
        <div class="panel panel-default">
          <div class="panel-body">
            <form class="form-inline" id="add" v-on:submit.prevent="addUser">
              <el-col :sx="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="gioitinh">Giới Tính</label>
                <el-select class="fullform" v-model="userupdate.gioitinh" placeholder="Select">
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
                <label for="GoiTap">Họ và Tên</label>
                <el-input class="fullform"
                  placeholder="Please Input"
                  v-model="userupdate.name">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày sinh</label>
                <input class="form-group" type="date" v-model="userupdate.birthday">
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Địa chỉ</label>
                <el-input class="fullform"
                  placeholder="Please Input"
                  v-model="userupdate.diachi">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày phát hành</label>
                <input class="form-group" type="date" v-model="userupdate.phathanh">
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Ngày gia hạn</label>
                <input class="form-group" type="date" v-model="userupdate.giahan">
              </div>
            </el-col>
            <el-col :xs="24" :sm="12" :md="6">
              <div class="form-group">
                <label for="GoiTap">Số tháng đóng</label>
                <el-input class="fullform"
                  placeholder="Please Input"
                  v-model="userupdate.sothang">
                </el-input>
              </div>
            </el-col>
            <el-col :xs="24" :sm="24" :md="24">
            <el-button v-on:click="updateUser"type="primary">Primary Button</el-button>
            </el-col>
            </form>
          </div>
        </div>
      </el-col>
    </el-row>
    <div class="page-header">
      <h1>{{msg}}</h1>
    </div>
    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>All User</h3>
        <form class="group-inline" id="search" v-cloak>
          <div class="form-group">
            <input type="text" v-model="searchString" placeholder="Nhập tên cần tìm">
          </div>
        </form>
      </div>
      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>STT</th>
              <th>Mã KH</th>
              <th>Gói tập</th>
              <th>Lớp</th>
              <th>Họ và Tên</th>
              <th>Ngày Sinh</th>
              <th>Giới tính</th>
              <th>Địa chỉ</th>
              <th>Ngày phát hành</th>
              <th>Ngày gia hạn</th>
              <th>Số tháng đóng</th>
              <th>Ngày hết hạn</th>
              <th>Trạng thái</th>
              <th>Cập nhât</th>
              <th>Ẩn</th>
            </tr>
          </thead>
            <transition-group name="fade"  tag="tbody">
            <tr class="user" v-if="!user.checked" v-for="user in filterUser" v-bind:key="user" >
              <td>{{user.stt}}</td>
              <td>{{user.makh}}</td>
              <td>{{user.goi}}</td>
              <td>{{user.lop}}</td>
              <td>{{user.name}}</td>
              <td>{{user.birthday}}</td>
              <td>{{user.gioitinh}}</td>
              <td>{{user.diachi}}</td>
              <td>{{user.phathanh}}</td>
              <td>{{user.giahan}}</td>
              <td>{{user.sothang}}</td>
              <td>{{user.hethan}}</td>
              <td>{{user.trangthai}}</td>
              <td><span class="glyphicon glyphicon-pencil updatefun" v-on:click="update(user)"></span>
              </td>
              <td><label class="switch" >
              <input v-on:click="check(user)" type="checkbox" id="checkbox" v-model="user.checked" checked>
              <div class="slider round"></div>
              </label></td>
            </tr>
          </transition-group>

        </table>
      </div>
    </div>
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

export default {
  name: 'hello',
  components: {
    'vue-datetime-picker': require('vue-datetime-picker')
  },
  firebase: {
    listuser: danhsachref
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
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
        sothang: '',
        giahan: '',
        hethan: '',
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
      key1: '',
      key2: ''
    }
  },
  computed: {
    filterUser: function () {
      console.log(this.listuser)
      var ngayhientai = moment().date()
      var thanghientai = moment().month() + 1
      var namhientai = moment().year()
      var articlearray = this.listuser.map(function (item) {
        if ((ngayhientai >= moment(item.hethan).date()) && (thanghientai >= moment(item.hethan).month() + 1) && (namhientai >= moment(item.hethan).year())) {
          if (ngayhientai >= moment(item.hethan).date()) {
            console.log('dau tien')
          }
          item.trangthai = 'Đã hết hạn'
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
    }
  },
  methods: {
    addUser: function () {
      var dategiahan = moment(this.newuser.giahan)
      // var parts = dategiahan.match(/(\d+)/g)
      // var dateafterconvert = new Date(parts[0], parts[1] - 1, parts[2])
      console.log(moment(dategiahan).format('DD/MM/YYYY'))
      var x = moment(dategiahan).format('DD/MM/YYYY')
      var y = moment(dategiahan).format('L')
      var datephathanh = moment(this.newuser.phathanh)
      var xph = moment(datephathanh).format('DD/MM/YYYY')
      console.log(xph)
      this.newuser.phathanh = xph
      var ngaygiahan = moment(dategiahan).date()
      var thanggiahan = moment(dategiahan).month() + 1
      var namgiahan = moment(dategiahan).year()
      console.log('Ngay ' + ngaygiahan + ' Thang ' + thanggiahan + ' Nam ' + namgiahan)
      console.log(ngaygiahan)
      this.newuser.giahan = x
      var getdate = moment(y).add(30 * this.newuser.sothang, 'days')
      var datehethan = moment(getdate).format('DD/MM/YYYY')
      console.log(datehethan)
      this.newuser.hethan = datehethan
      this.newuser.stt = this.listuser.length + 1
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
      var dategiahan = moment(this.userupdate.giahan)
      var x = moment(dategiahan).format('L')
      var y = moment(dategiahan).format('DD/MM/YYYY')
      var datephathanh = moment(this.userupdate.phathanh)
      var xph = moment(datephathanh).format('DD/MM/YYYY')
      this.userupdate.phathanh = xph
      var getdate = moment(x).add(30 * this.userupdate.sothang, 'days')
      var datehethan = moment(getdate).format('DD/MM/YYYY')
      this.userupdate.hethan = datehethan
      this.userupdate.giahan = y
      delete this.userupdate['.key']
      danhsachref.child(this.key2).set(this.userupdate)
      this.userupdate = ''
    },
    showadduser: function () {
      this.checkadd = true
    },
    doneadduser: function () {
      this.checkadd = false
    },
    update: function (user) {
      this.userupdate = user
      this.userupdate.phathanh = moment(user.phathanh).format('YYYY-MM-DD')
      this.userupdate.giahan = moment(user.giahan).format('YYYY-MM-DD')
      console.log(this.userupdate.phathanh)
      console.log(this.userupdate.giahan)
      this.key1 = user['.key']
      if (this.key1 != null) {
        this.key2 = this.key1
      }
      console.log(this.key1)
      console.log(this.key2)
      this.checkupdate = true
      console.log(user.giahan)
    },
    check: function (user) {
      var key = user['.key']
      delete user['.key']
      danhsachref.child(key).set(user)
      console.log('check')
      console.log(user.checked)
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
.fullform {
  width: 100%;
}
.form-group {
  width:100%;
}
.addbtn {
  width:50px;
  height:50px;
  border-radius: 50%;
  float: right;
  margin-right: 50px;
}
li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
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
.user {
  transition: 1s;
}
/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0
}
.updatefun {
  cursor: pointer;
}
.slider.round:before {
  border-radius: 50%;
}
</style>
