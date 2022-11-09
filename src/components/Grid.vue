<script>
import.meta.env;

export default {
  props: ["results", "showGrid"],
};
</script>

<template>
  <div class="container bg-red">
    <table class="table" v-show="showGrid">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Teacher Key</th>
          <th scope="col">Student Answer</th>
          <th scope="col">Score</th>
          <th scope="col">Match?</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, index) in results.reverse()"
          style="vertical-align: middle"
        >
          <th scope="row">{{ (index += 1) }}</th>
          <td>{{ item.key }}</td>
          <td>{{ item.answer }}</td>
          <td>{{ parseFloat(item.score * 100).toFixed(2) }}%</td>
          <td>
            <p
              class="p-1 px-3 rounded"
              style="width: fit-content; margin: 0px"
              :style="
                item.likelyhood
                  ? { backgroundColor: 'lightgreen' }
                  : { backgroundColor: 'red' }
              "
            >
              {{ item.likelyhood ? "Yes" : "No" }}
            </p>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
