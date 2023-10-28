<script>
  let paling_sedikit = "";
  let paling_banyak = "";
  let hasil = "";

  function bagiDenganDelapanDanHasilkanArray(n) {
    const result = [];
    let sisa = n % 8;
    const bagianBulat = Math.floor(n / 8);

    for (let i = 0; i < 8; i++) {
      if (i < sisa) {
        result.push(bagianBulat + 1);
      } else {
        result.push(bagianBulat);
      }
    }

    return result;
  }

  function buatRentang(angka, interval) {
    if (interval == 1) {
      return angka;
    } else if (interval == 0) {
      return null;
    } else {
      return `${angka - interval + 1} - ${angka}`;
    }
  }

  function generateIntervals() {
    let banyaknya = paling_banyak - paling_sedikit + 1;
    let array_delapan = bagiDenganDelapanDanHasilkanArray(banyaknya);

    let kelompok_angka = [];
    let angka_terakhir = paling_banyak;
    for (let x of array_delapan) {
      kelompok_angka = [...kelompok_angka, +angka_terakhir];
      angka_terakhir -= x;
    }

    let rentangnya = [];
    for (let n in kelompok_angka) {
      rentangnya = [
        ...rentangnya,
        buatRentang(kelompok_angka[n], array_delapan[n]),
      ];
    }

    hasil = rentangnya.join("\n");
  }

  $: if (paling_sedikit || paling_banyak) {
    generateIntervals();
  }
</script>

<div class="pt-3">
  <div class="form-control w-full">
    <label class="label">
      <span class="label-text">Paling Sedikit</span>
    </label>
    <input
      type="tel"
      bind:value={paling_sedikit}
      placeholder="1"
      class="input input-bordered w-full"
    />
  </div>
  <div class="form-control w-full">
    <label class="label">
      <span class="label-text">Paling Banyak</span>
    </label>
    <input
      type="tel"
      bind:value={paling_banyak}
      placeholder="10"
      class="input input-bordered w-full"
    />
  </div>
  <textarea
    class="textarea textarea-bordered w-full mt-3"
    readonly
    bind:value={hasil}
    placeholder="Hasil"
    rows="10"
  />
</div>
