<template>
  <div class="p-2" style="overflow-x: hidden;">
    <h1 style="text-align: center;">ÜRÜN EKLEME UYGULAMASI</h1>

    <div class="row mt-4">
      <div class=" col-12 col-md-5">
        <div class="card p-4">

          <form>

            <h2 style="text-align: center;">Ürün Ekleme Sayfası</h2>
            <div class="row">
              <div class="col-md-4">
                <div class="form-group">
                  <label for="resimEkle">
                    <img id="output" class="col-md-12" style="width: 100%;" :src="defaultImage" alt="" srcset="">
                  </label>
                  <input type="file" id="fileInput" required @change="changeFile">
                </div>
              </div>
              <div class="col-md-8">
                <div class="form-group">
                  <label for="urunAdı">Ürün Adı</label>
                  <input type="text" class="form-control" required v-model="urunAdi" placeholder="xxxxx">
                </div>
                <div class="form-row">
                  <div class="form-group col-md-12">
                    <label for="urunAdet">Ürün Adeti</label>
                    <input type="number" class="form-control" required v-model="urunAdet" placeholder="xxxxx">
                  </div>
                  <div class="form-group col-md-12">
                    <label for="urunFiyat">Ürün Fiyatı</label>
                    <input type="number" class="form-control" required v-model="urunFiyat" placeholder="xxxxx">
                  </div>
                </div>
              </div>
              <div class="col-md-12">
                <button type="button" class="col-md-12 btn btn-success" @click="urunEkle()">Kaydet</button>
              </div>
            </div>

          </form>
        </div>
      </div>

      <div class=" col-12  col-md-7">
        <div class="card p-4 " style="height: 533px;max-height: 533px;overflow-y: auto;">

          <form>
            <h2 style="text-align: center;">Sepet Sayfası</h2>
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">Ürün Görsel</th>
                  <th scope="col">Ürün</th>
                  <th scope="col">Adet</th>
                  <th scope="col">Birim Fiyat</th>
                  <th scope="col">Toplam Fiyat</th>

                </tr>
              </thead>
              <tbody>
                <tr v-for="(sepet) in sepetUrunler">
                  <td><img style="width: 30px" :src="sepet.productImage" id="guncelSepetResim" alt=""></td>
                  <td>{{ sepet.productName }}</td>
                  <td>{{ sepet.productCount }}
                    <button type="button" style="background-color: greenyellow; border-radius: 5px;"
                      @click="adetEkle(sepet)"> + </button>
                    <button type="button" style="background-color: red; border-radius: 5px;" @click="adetCikar(sepet)">
                      - </button>
                  </td>
                  <td>{{ sepet.productPrice }}$ </td>
                  <td>{{ sepet.productCount * sepet.productPrice }}$</td>
                </tr>

              </tbody>
            </table>

          </form>


        </div>
      </div>
    </div>

    <div class="row mt-4">
      <div class="col-md-12  ">
        <div class="card">
          <h2 style="text-align: center; margin-top: 25px ">Ürünler Sayfası</h2>
          <table class="table">
            <thead>
              <tr>
                <th scope="col">Ürün Görsel</th>
                <th scope="col">Ürün</th>
                <th scope="col">Adet</th>
                <th scope="col">Birim Fiyat</th>
                <th scope="col"></th>
                <th scope="col"></th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(urun, index) in urunler">
                <td><img v-if="urun?.productImage" style="width: 30px" :src="urun?.productImage" alt=""></td>
                <td>{{ urun?.productName }}</td>
                <td>{{ urun?.productCount }}</td>
                <td>{{ urun?.productPrice }}$</td>
                <td><button class="btn btn-primary" @click="sepeteEkle(index)">Sepete Ekle</button></td>
                <td><button class="btn btn-warning" type="button" @click="guncelle(index)"
                    data-target="#exampleModalCenter" data-toggle="modal">Güncelle</button>
                </td>
              </tr>

            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

  <!-- MODAL -->
  <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle"
    aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title " id="exampleModalLongTitle">Ürün Güncelleme Sayfası</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form style="text-align: center; ">
            <div class="form-row">
              <div class="form-group col-md-6 ">
                <img style="width: 100px;" id="guncelUrunResim" alt="">
              </div>
              <div class="form-group col-md-6 ">
                <label>Ürün Resim</label>

                <input type="file" @change="GuncelChangeFile" />
              </div>
            </div>
            <div class="form-row">
              <div class="form-group col-md-12 ">
                <label for="guncelUrun">Ürün Adı</label>
                <input type="text" class="form-control" id="guncelUrun" v-model="guncelUrun.productName">
              </div>
            </div>
            <div class="form-row">
              <div class="form-group col-md-12 ">
                <label for="guncelUrunAdet">Ürün Adet</label>
                <input type="number" class="form-control" id="guncelUrunAdet" v-model="guncelUrun.productCount">
              </div>
            </div>
            <div class="form-row">
              <div class="form-group col-md-12 ">
                <label for="guncelUrunFiyat">Ürün Fiyat</label>
                <input type="number" class="form-control" id="guncelUrunFiyat" v-model="guncelUrun.productPrice">
              </div>
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary" @click="urunuGuncelle()">Ürünü Güncelle</button>
        </div>
      </div>
    </div>
  </div>

  <!-- MODAL 2 -->
  <!-- Button trigger modal -->

  <div class="" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true"
    v-show="login">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">DİKKAT!!!</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">

          </button>
        </div>
        <div class="modal-body">
          <p style="font-size: large;">Sepette Aynı Üründen Bulunuyor, Nasıl Eklemek İstersiniz?
          </p>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-success" data-dismiss="modal" @click="yeniUrunEkle()">YENİ ÜRÜN
            EKLE</button>
          <button type="button" class="btn btn-warning" data-dismiss="modal" @click="yeniAdetEkle()">ADET
            EKLE</button>
          <button type="button" class="btn btn-danger" @click="login = false">İPTAL</button>
        </div>
      </div>
    </div>
  </div>


</template>

<script>
import image from "./assets/image/QR.jpg"

export default {
  data() {
    return {
      login: false,
      addfile: "",
      updatefile: "",
      urunAdi: "",
      urunAdet: "",
      urunFiyat: "",
      urunler: [],
      sepetUrunler: [],
      guncelUrun: [],
      silinecek: [],
      indexFind: null,
      sepetFind: null,
      defaultImage: image

    }
  },
  methods: {
    changeFile(event) {
      this.addfile = event.target.files[0]
      document.getElementById('output').src = window.URL.createObjectURL(this.addfile)
    },
    GuncelChangeFile(event) {
      this.updatefile = event.target.files[0]
      document.getElementById('guncelUrunResim').src = window.URL.createObjectURL(this.updatefile)
    },
  
    sifirlama() {
      this.urunAdi = ""
      this.urunAdet = "",
        this.urunFiyat = "",
        this.addfile = "",
        document.getElementById('fileInput').value = '';
      document.getElementById('output').src = this.defaultImage;
    },
    yeniUrunEkle() {
      this.urunler.push({ productId: Math.random(10), productName: this.urunAdi, productImage: window.URL.createObjectURL(this.addfile), productCount: this.urunAdet, productPrice: this.urunFiyat })
      this.sifirlama()
      this.login = false
    },
    yeniAdetEkle() {
      let eklenenUrunAdi = this.urunler.filter(name => name.productName == this.urunAdi)
      eklenenUrunAdi[0].productName = this.urunAdi
      eklenenUrunAdi[0].productCount += this.urunAdet
      eklenenUrunAdi[0].productPrice = this.urunFiyat
      this.sifirlama()
      this.login = false
    },
    urunEkle() {
      if (!this.urunAdi || !this.urunAdet || !this.urunFiyat || !document.getElementById('fileInput').value) {
        alert("Lütfen tüm alanları doldurun!");
        return;
      }
      else {
        let eklenenUrunAdi = this.urunler.filter(name => name.productName == this.urunAdi)
        if (eklenenUrunAdi.length > 0) {
          this.login = true
        } else {
          this.urunler.push({ productId: Math.random(10), productName: this.urunAdi, productImage: window.URL.createObjectURL(this.addfile), productCount: this.urunAdet, productPrice: this.urunFiyat })
          this.sifirlama()
          this.login = false
        }
      }
    },
    sepeteEkle(index) {
      const a = this.urunler[index]
      let eklenenUrunId = this.sepetUrunler.filter(id => id.productId == a.productId)

      if (a.productCount > 0) {
        if (eklenenUrunId.length == 1) {
          this.sepetUrunler[index].productCount++
        } else {
          this.sepetUrunler.push({
            productId: a.productId,
            productImage: a.productImage,
            productName: a.productName,
            productCount: 1,
            productPrice: a.productPrice
          })
        }
        a.productCount--

      } else {
        alert("Bu Üründen Daha Fazla Ekleyemezsin!!!")
      }

    },

    guncelle(index) {
      this.indexFind = null;
      document.getElementById('guncelUrunResim').src = this.urunler[index].productImage
      this.guncelUrun = JSON.parse(JSON.stringify(this.urunler[index]))
      this.indexFind = this.guncelUrun.productId;
    },
    urunuGuncelle() {
      this.urunler.map(bul => {
        if (bul.productId === this.indexFind) {
          bul.productName = this.guncelUrun.productName,
            bul.productCount = this.guncelUrun.productCount,
            bul.productPrice = this.guncelUrun.productPrice,
            bul.productImage = document.getElementById('guncelUrunResim').src
          // if (this.guncelUrun.productImage == null) {
          //   bul.productImage = window.URL.createObjectURL(this.updatefile)
          // }
          // console.log("güncel ürün fiyatının lenght",this.guncelUrun.productPrice)

          // console.log("güncel ürün",this.guncelUrun)
          // console.log("güncel ürün fiyatı",this.guncelUrun.productPrice)
          // if(this.guncelUrun.productPrice == null){
          //   console.log("demekki boş")
          // }

        }
      });
      this.sepetUrunler.map(degis => {
        if (degis.productId === this.guncelUrun.productId) {
          degis.productName = this.guncelUrun.productName,
            degis.productCount = degis.productCount,
            degis.productPrice = this.guncelUrun.productPrice
          if (this.guncelUrun == true) {
            degis.productImage = window.URL.createObjectURL(this.updatefile)
          }
          degis.productImage = document.getElementById('guncelUrunResim').src
        }
      });
      $('#exampleModalCenter').modal('hide');
    },

    adetEkle(sepet) {
      this.urunler.map(ara => {
        if (ara.productId === sepet.productId) {
          if (ara.productCount > 0) {
            sepet.productCount++
            ara.productCount--
          } else {
            alert("Bu Üründen Daha Fazla Stokta Yok")
          }
        }

      });

    },
    adetCikar(sepet) {
      this.urunler.map(ara => {
        if (ara.productId === sepet.productId) {
          sepet.productCount--
          if (sepet.productCount >= 0) {

            ara.productCount++
            if (sepet.productCount == 0) {
              console.log("sepetteki  ürünler", sepet)
              console.log("çıkarılan ürün", sepet.productId)
              console.log("this.sepetUrunler", this.sepetUrunler)


              this.sepetUrunler = this.sepetUrunler.filter(bul => { bul.productId !== sepet.productId })
            }
          }
        }
      });
    }
  }
}
</script>