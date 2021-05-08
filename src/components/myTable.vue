  <template>
  <div class="main">
    <el-table
      :data="tableData"
      id="table"
      row-key="id"
      style="width: 100%"
      :border="true"
    >
      <el-table-column
        v-for="(item, index) in col"
        :key="`col_${index}`"
        :prop="dropCol[index].prop"
        :label="item.label"
      >
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import Sortable from "sortablejs";
export default {
  data() {
    return {
      col: [
        {
          label: "日期",
          prop: "date",
        },
        {
          label: "姓名",
          prop: "name",
        },
        {
          label: "地址",
          prop: "address",
        },
      ],
      dropCol: [
        {
          label: "日期",
          prop: "date",
        },
        {
          label: "姓名",
          prop: "name",
        },
        {
          label: "地址",
          prop: "address",
        },
      ],
      tableData: [
        {
          id: "1",
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          id: "2",
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄",
        },
        {
          id: "3",
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄",
        },
        {
          id: "4",
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄",
        },
      ],
    };
  },
  mounted() {
    this.rowDrop();
    this.columnDrop();
  },
  methods: {
    rowDrop() {
      const tbody = document.querySelector("#table tbody");
      const _this = this;
      Sortable.create(tbody, {
        onEnd({ newIndex, oldIndex }) {
          const currRow = _this.tableData.splice(oldIndex, 1)[0];
          _this.tableData.splice(newIndex, 0, currRow);
        },
      });
    },
    columnDrop() {
      const wrapperTr = document.querySelector("#table tr");
      this.sortable = Sortable.create(wrapperTr, {
        animation: 180,
        delay: 0,
        onEnd: (evt) => {
          const oldItem = this.dropCol[evt.oldIndex];
          this.dropCol.splice(evt.oldIndex, 1);
          this.dropCol.splice(evt.newIndex, 0, oldItem);
        },
      });
    },
  },
};
</script>

<style scoped>
.main {
  width: 800px;
  margin: 0 auto;
  margin-top: 300px;
}
</style>