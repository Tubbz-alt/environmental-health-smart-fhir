<template>
  <div>
    <div class="tabs is-centered">
      <ul>
        <li :class="{ 'is-active': view === 'summary' }" @click="toggleView('summary')"><a>Air Quality Indicators (AQI)</a></li>
        <li :class="{ 'is-active': view === 'daily' }" @click="toggleView('daily')"><a>Daily AQI for Encounters</a></li>
        <li :class="{ 'is-active': view === 'patientinfo' }" @click="toggleView('patientinfo')"><a>Inform Patient</a></li>
        <li :class="{ 'is-active': view === 'asthmaSeverity' }" @click="toggleView('asthmaSeverity')"><a>Calculate Asthma Severity</a></li>
      </ul>
    </div>
    <p-m25-visualization v-if="view === 'summary'" :patient="patient"></p-m25-visualization>
    <encounters-air-quality :encounters="encounters" v-else-if="view === 'daily'" :patient="patient" ></encounters-air-quality>
    <patient-info v-else-if="view==='patientinfo'"></patient-info>
    <asthma-severity v-else-if="view==='asthmaSeverity'" :patient="patient"></asthma-severity>
  </div>

</template>

<script>
import PM25Visualization from './PM25Visualization';
import AirNow from './AirNow';
import AsthmaSeverity from './AsthmaSeverity';
import EncountersAirQuality from './EncountersAirQuality';
import PatientInfo from './PatientInfo';

export default {
  name: 'air-quality-asthma-tabs',
  components: {
    AirNow,
    AsthmaSeverity,
    PM25Visualization,
    EncountersAirQuality,
    PatientInfo
  },
  props: {
    patient: {
      type: Object
    },
    encounters: {
      type: Array
    }
  },
  data() {
    return {
      view: 'summary' // or daily
    };
  },
  methods: {
    toggleView(view) {
      this.view = view;
    }
  }
};
</script>
