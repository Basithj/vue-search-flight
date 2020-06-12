<template>
  <div>
    <b-card class="mt-3" header="Booking Summary">
      <b-list-group>
        <b-list-group-item><b>Origin:</b> {{ origin }}</b-list-group-item>
        <b-list-group-item><b>Destination:</b> {{ destination }}</b-list-group-item>
        <b-list-group-item><b>Aircraft:</b> {{ aircraft }}</b-list-group-item>
        <b-list-group-item><b>Passenger:</b> {{ passenger }}</b-list-group-item>
        <b-list-group-item><b>Desired Date:</b> {{ desireddate }}</b-list-group-item>
      </b-list-group>
    </b-card>
  </div>
</template>

<script>
export default {
  props: [ 
    'origin',
    'destination',
    'aircraft',
    'passenger',
    'desireddate'
  ]
}
</script>
