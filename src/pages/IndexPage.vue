<template>
  <q-page class="">
    <div class="q-pa-md">
      <div class="row justify-around">
        <div class="col-12 col-md-4 q-gutter-x-md">
          <div class="q-pa-md">
            <div class="q-gutter-y-md column left_inputs">
              <div class="inputs">
                <label>Quantity</label>
                <input
                  v-model="quantity"
                  type="number"
                  placeholder="Quantity"
                  required
                />
                <label>Unit Price</label>
                <input
                  v-model="unit_price"
                  type="number"
                  placeholder="Price"
                  required
                />
                <label>Freight</label>
                <input
                  v-model="freight"
                  type="number"
                  placeholder="Freight"
                  required
                />
                <!-- <label>Insurance</label>
                <input
                  v-model="insurance"
                  type="number"
                  placeholder="Insurance"
                  required
                /> -->
                <label>Import Excise Duty Rate</label>
                <input
                  v-model="import_excise_duty_rate"
                  type="number"
                  placeholder="Excise Duty Rate"
                  required
                />

                <label>Import Duty Rate</label>
                <input
                  v-model="import_duty_rate"
                  type="number"
                  placeholder="Import Duty Rate"
                  required
                />
                <q-separator class="q-my-md"></q-separator>
                <label>Exchange Rate</label>
                <input
                  v-model="exchange_rate"
                  type="number"
                  placeholder="Exchange Rate"
                  required
                />
              </div>
            </div>
          </div>
        </div>
        <div class="col-12 col-md-8">
          <div class="q-pa-md">
            <q-markup-table>
              <thead>
                <tr class="bg-grey-3">
                  <th class="text-left">Tax Codes</th>
                  <th class="text-left">Tax Description</th>
                  <th class="text-right">Tax $USD</th>
                  <th class="text-right">Tax GHS</th>
                </tr>
              </thead>
              <tbody>
                <tr style="color: gray">
                  <td class="text-left"></td>
                  <td class="text-left">FOB</td>
                  <td v-show="FOB" class="text-right">{{ FOB.toFixed(2) }}</td>
                  <td v-show="FOB" class="text-right">
                    {{ (FOB * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr style="color: gray">
                  <td class="text-left"></td>
                  <td class="text-left">CIF</td>
                  <td v-show="CIF" class="text-right">{{ CIF.toFixed(2) }}</td>
                  <td v-show="CIF" class="text-right">
                    {{ (CIF * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">01</td>
                  <td class="text-left">Import Duty</td>
                  <td v-show="importDuty" class="text-right">
                    {{ importDuty.toFixed(2) }}
                  </td>
                  <td v-show="importDuty" class="text-right">
                    {{ (importDuty * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">02</td>
                  <td class="text-left">Import VAT</td>
                  <td v-show="importVAT" class="text-right">
                    {{ importVAT.toFixed(2) }}
                  </td>
                  <td v-show="importVAT" class="text-right">
                    {{ (importVAT * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">04</td>
                  <td class="text-left">Import excise duty</td>
                  <td v-show="importExciseDuty" class="text-right">
                    {{ importExciseDuty.toFixed(2) }}
                  </td>
                  <td v-show="importExciseDuty" class="text-right">
                    {{ (importExciseDuty * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">06</td>
                  <td class="text-left">ECOWAS Levy</td>
                  <td v-show="ECOWASLevy" class="text-right">
                    {{ ECOWASLevy.toFixed(2) }}
                  </td>
                  <td v-show="ECOWASLevy" class="text-right">
                    {{ (ECOWASLevy * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">32</td>
                  <td class="text-left">Network Charge</td>
                  <td v-show="networkCharge" class="text-right">
                    {{ networkCharge.toFixed(2) }}
                  </td>
                  <td v-show="networkCharge" class="text-right">
                    {{ (networkCharge * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">33</td>
                  <td class="text-left">Network Charge VAT</td>
                  <td v-show="networkChargeVAT" class="text-right">
                    {{ networkChargeVAT.toFixed(2) }}
                  </td>
                  <td v-show="networkChargeVAT" class="text-right">
                    {{ (networkChargeVAT * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">39</td>
                  <td class="text-left">Network Charge COVID-19</td>
                  <td v-show="networkChargeCOVID" class="text-right">
                    {{ networkChargeCOVID.toFixed(2) }}
                  </td>
                  <td v-show="networkChargeCOVID" class="text-right">
                    {{ (networkChargeCOVID * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">47</td>
                  <td class="text-left">Import NHIL</td>
                  <td v-show="importNHIL" class="text-right">
                    {{ importNHIL.toFixed(2) }}
                  </td>
                  <td v-show="importNHIL" class="text-right">
                    {{ (importNHIL * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">48</td>
                  <td class="text-left">Network Charge NHIL</td>
                  <td v-show="networkChargeNHIL" class="text-right">
                    {{ networkChargeNHIL.toFixed(2) }}
                  </td>
                  <td v-show="networkChargeNHIL" class="text-right">
                    {{ (networkChargeNHIL * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">56</td>
                  <td class="text-left">IRS Tax Deposit</td>
                  <td v-show="IRS_TaxDeposit" class="text-right">
                    {{ IRS_TaxDeposit.toFixed(2) }}
                  </td>
                  <td v-show="IRS_TaxDeposit" class="text-right">
                    {{ (IRS_TaxDeposit * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">78</td>
                  <td class="text-left">Special Import Levy</td>
                  <td v-show="specialImportLevy" class="text-right">
                    {{ specialImportLevy.toFixed(2) }}
                  </td>
                  <td v-show="specialImportLevy" class="text-right">
                    {{ (specialImportLevy * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">87</td>
                  <td class="text-left">Ghana EXIM Levy</td>
                  <td v-show="EXIMLevy" class="text-right">
                    {{ EXIMLevy.toFixed(2) }}
                  </td>
                  <td v-show="EXIMLevy" class="text-right">
                    {{ (EXIMLevy * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">88</td>
                  <td class="text-left">GETFUND Import Levy</td>
                  <td v-show="importGETFUND" class="text-right">
                    {{ importGETFUND.toFixed(2) }}
                  </td>
                  <td v-show="importGETFUND" class="text-right">
                    {{ (importGETFUND * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">89</td>
                  <td class="text-left">Network Charge GETFUND</td>
                  <td v-show="networkChargeGETFUND" class="text-right">
                    {{ networkChargeGETFUND.toFixed(2) }}
                  </td>
                  <td v-show="networkChargeGETFUND" class="text-right">
                    {{ (networkChargeGETFUND * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">93</td>
                  <td class="text-left">Inspection Fee</td>
                  <td v-show="inspectionFee" class="text-right">
                    {{ inspectionFee.toFixed(2) }}
                  </td>
                  <td v-show="inspectionFee" class="text-right">
                    {{ (inspectionFee * exchangeRate).toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="text-left">98</td>
                  <td class="text-left">AU Import Levy</td>
                  <td v-show="AU_importLevy" class="text-right">
                    {{ AU_importLevy.toFixed(2) }}
                  </td>
                  <td v-show="AU_importLevy" class="text-right">
                    {{ (AU_importLevy * exchangeRate).toFixed(2) }}
                  </td>
                </tr>

                <tr
                  style="
                    font-weight: bold;
                    color: white;
                    background-color: green;
                  "
                >
                  <td class="text-left">TOTAL DUTY</td>
                  <td class="text-left">
                    1 USD =<span v-show="exchange_rate">
                      GHS {{ exchangeRate }}</span
                    >
                  </td>
                  <td v-if="TOTAL_DUTY" class="text-right">
                    $ {{ TOTAL_DUTY.toFixed(2) }}
                  </td>
                  <td v-else class="text-right">$ {{ 0 }}</td>

                  <td v-if="TOTAL_DUTY_IN_CEDIS" class="text-right">
                    GHS {{ TOTAL_DUTY_IN_CEDIS.toFixed(2) }}
                  </td>
                  <td v-else class="text-right">GHS {{ 0 }}</td>
                </tr>
              </tbody>
            </q-markup-table>

            <div class="q-gutter-y-md column" style="width: 500px">
              <!-- <h5 v-if="TOTAL_DUTY">Total Duty: {{ TOTAL_DUTY }}</h5>
              <p>FOB: {{ FOB }}</p>
              <p>CIF: {{ CIF }}</p>
              <p>import excise duty: {{ importExciseDuty }}</p>
              <p>import duty: {{ importDuty }}</p>
              <p>import NHIL: {{ importNHIL }}</p>
              <p>import GETFUND: {{ importGETFUND }}</p>
              <p>import COVID-19 Levy: {{ importCOVID }}</p>
              <p>import VAT: {{ importVAT }}</p>
              <p>ECOWAS Levy: {{ ECOWASLevy }}</p>
              <p>Network Charge: {{ networkCharge }}</p>
              <p>Network Charge NHIL: {{ networkChargeNHIL }}</p>
              <p>Network Charge GETFUND: {{ networkChargeGETFUND }}</p>
              <p>Network Charge COVID-19 HRL: {{ networkChargeCOVID }}</p>
              <p>Network Charge VAT: {{ networkChargeVAT }}</p>
              <p>IRS Tax Deposit: {{ IRS_TaxDeposit }}</p>
              <p>Special Import Levy: {{ specialImportLevy }}</p>
              <p>Ghana EXIM Levy: {{ EXIMLevy }}</p>
              <p>Inspection Fee: {{ inspectionFee }}</p>
              <p>AU Import Levy: {{ AU_importLevy }}</p> -->
              <!-- <button type="submit">Calculate</button> -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      exchange_rate: null,
      unit_price: null,
      quantity: null,
      freight: null,
      // insurance: null,
      import_excise_duty_rate: null,
      import_duty_rate: null,
    };
  },
  methods: {
    // convert(unit_price, quantity){
    //     return unit_price * quantity
    // }
    // ,
  },
  computed: {
    FOB() {
      const price = parseFloat(this.unit_price);
      if (price == null) {
        return 0;
      }

      const quantity = parseInt(this.quantity);
      const totalPrice = price * quantity;
      return totalPrice;
    },
    insurance() {
      const rate = 0.875 / 100;
      const freight = this.freight;
      const insurance = rate * (this.FOB + freight);
      return insurance;
    },
    CIF() {
      const freight = parseFloat(this.freight);
      const insurance = parseFloat(this.insurance);
      return this.FOB + freight + insurance;
    },
    importExciseDuty() {
      const rate = parseFloat(this.import_excise_duty_rate / 100);
      if (rate == 0) {
        console.log(rate);
        return 0;
      }
      console.log(rate * this.CIF);
      console.log(rate);
      return rate * this.CIF;
    },
    importDuty() {
      const rate = parseFloat(this.import_duty_rate / 100);
      return rate * this.CIF;
    },
    CIF_ID_EXD() {
      const CIF_ID_EXD = this.CIF + this.importDuty + this.importExciseDuty;
      return CIF_ID_EXD;
    },
    importNHIL() {
      const NHIL = (2.5 / 100) * this.CIF_ID_EXD;
      console.log(NHIL);
      return NHIL;
    },
    importGETFUND() {
      const GETFUND = (2.5 / 100) * this.CIF_ID_EXD;
      console.log(GETFUND);
      return GETFUND;
    },
    importCOVID() {
      const COVID = (1 / 100) * this.CIF_ID_EXD;
      console.log(COVID);
      return COVID;
    },
    importVAT() {
      const VAT =
        (12.5 / 100) *
        (this.CIF_ID_EXD +
          this.importNHIL +
          this.importGETFUND +
          this.importCOVID);

      return VAT;
    },
    ECOWASLevy() {
      const ECOWASLevy = (0.5 / 100) * this.CIF;

      return ECOWASLevy;
    },
    networkCharge() {
      const networkCharge = (0.4 / 100) * this.FOB;
      if (this.FOB == null) {
        return 0;
      } else {
        return networkCharge;
      }
    },
    networkChargeNHIL() {
      const networkChargeNHIL = (2.5 / 100) * this.networkCharge;
      if (this.networkCharge == null) {
        return 0;
      } else {
        return networkChargeNHIL;
      }
    },
    networkChargeGETFUND() {
      const networkChargeGETFUND = (2.5 / 100) * this.networkCharge;

      return networkChargeGETFUND;
    },
    networkChargeCOVID() {
      const networkChargeCOVID = (1 / 100) * this.networkCharge;

      return networkChargeCOVID;
    },
    networkChargeVAT() {
      const rate = 12.5 / 100;
      const totalNetworkCharge =
        this.networkCharge +
        this.networkChargeNHIL +
        this.networkChargeGETFUND +
        this.networkChargeCOVID;
      const networkChargeVAT = rate * totalNetworkCharge;
      return networkChargeVAT;
    },
    IRS_TaxDeposit() {
      const IRS_TaxDeposit = (1 / 100) * this.CIF;

      return IRS_TaxDeposit;
    },
    specialImportLevy() {
      const specialImportLevy = (2 / 100) * this.CIF;

      return specialImportLevy;
    },
    EXIMLevy() {
      const EXIMLevy = (0.75 / 100) * this.CIF;

      return EXIMLevy;
    },
    inspectionFee() {
      const inspectionFee = (1 / 100) * this.CIF;

      return inspectionFee;
    },
    AU_importLevy() {
      const AU_importLevy = (0.2 / 100) * this.CIF;

      return AU_importLevy;
    },
    TOTAL_DUTY() {
      if (this.CIF == null) {
        return 0;
      }
      const total =
        this.importDuty +
        this.importVAT +
        this.importExciseDuty +
        this.ECOWASLevy +
        this.networkCharge +
        this.networkChargeVAT +
        this.networkChargeCOVID +
        this.importNHIL +
        this.networkChargeNHIL +
        this.IRS_TaxDeposit +
        this.specialImportLevy +
        this.EXIMLevy +
        this.importGETFUND +
        this.networkChargeGETFUND +
        this.inspectionFee +
        this.AU_importLevy;
      return total;
    },
    exchangeRate() {
      const rate = parseFloat(this.exchange_rate);
      if (!this.exchange_rate) {
        return 0;
      } else {
        return rate;
      }
    },
    TOTAL_DUTY_IN_CEDIS() {
      const totalDuty = this.TOTAL_DUTY;
      const exchangeRate = this.exchangeRate;
      return totalDuty * exchangeRate;
    },
  },
  mounted() {},
};
</script>

<style scoped>
.left_inputs {
  /* width: 500px; */
}

@media screen and (max-width: 600px) {
  .container {
    width: 300px;
  }
}

.form__container {
  margin: 0;
  width: 100vw;
  background: #ecf0f3;
  display: flex;
  align-items: center;
  text-align: center;
  justify-content: center;
  place-items: center;
  overflow: auto;
}

.container {
  position: relative;
  margin: 3rem 0;
  width: 400px;
  /* height: 80%; */
  border-radius: 20px;
  padding: 40px;
  box-sizing: border-box;
  background: #ecf0f3;
  /* box-shadow: 14px 14px 20px #cbced1, -14px -14px 20px white; */
}

@media screen and (min-width: 650px) {
  .container {
    width: 500px;
  }
}

.brand-logo {
  height: 100px;
  width: 100px;
  background: url("https://img.icons8.com/color/100/000000/twitter--v2.png");
  margin: auto;
  border-radius: 50%;
  box-sizing: border-box;
  box-shadow: 7px 7px 10px #cbced1, -7px -7px 10px white;
}

.brand-title {
  margin-top: 10px;
  font-weight: 900;
  font-size: 1.3rem;
  color: var(--color-dark);
  letter-spacing: 1px;
}

.inputs {
  text-align: left;
  margin-top: 20px;
  width: 100%;
}

label,
input,
button {
  display: block;
  width: 100%;
  padding: 0;
  border: none;
  outline: none;
  box-sizing: border-box;
}

label {
  margin-bottom: 4px;
}

label:nth-of-type(2) {
  margin-top: 12px;
}

input::placeholder {
  color: gray;
}

input {
  background: #ecf0f3;
  margin-bottom: 1rem;
  padding: 10px;
  padding-left: 20px;
  height: 50px;
  font-size: 14px;
  border-radius: 10px;
  box-shadow: inset 6px 6px 6px #cbced1, inset -6px -6px 6px white;
}

button {
  color: white;
  margin-top: 20px;
  background: #1da1f2;
  height: 40px;
  border-radius: 20px;
  cursor: pointer;
  font-weight: 900;
  box-shadow: 6px 6px 6px #cbced1, -6px -6px 6px white;
  transition: 0.5s;
}

button:hover {
  box-shadow: none;
}

a {
  position: absolute;
  font-size: 8px;
  bottom: 4px;
  right: 4px;
  text-decoration: none;
  color: black;
  background: yellow;
  border-radius: 10px;
  padding: 2px;
}

h1 {
  position: absolute;
  top: 0;
  left: 0;
}
</style>
