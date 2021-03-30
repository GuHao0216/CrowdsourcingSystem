
<template>
  <div>
    <Card shadow title="任务管理">
      <row class="task-page" :gutter="32">
        <div class="task-page-other">
            <div style="margin-bottom:6px;">
          <Button
            to="https://zhuanlan.zhihu.com/feview"
            target="_blank"
            size="large"
          >
            新建任务
          </Button>
          <Button
            to="https://zhuanlan.zhihu.com/feview"
            target="_blank"
            size="large"
          >
            刷新
          </Button>
          </div>
          <tables
            ref="tables"
            v-model="tableData"
            :columns="columns"
            @on-delete="handleDelete"
          />
        </div>
      </row>
    </Card>
  </div>
</template>

<script>
import Tables from "_c/tables";
import { getTableData } from "@/api/data";
export default {
  name: "task_page",
    components: {
    Tables
  },
  data() {
    return {
      columns: [
        { title: "任务名称", key: "name", sortable: true },
        { title: "任务类型", key: "type", editable: true },
        { title: "发布情况", key: "publish" },
        { title: "总答案数", key: "totalAnswerNum",sortable: true },
        // { title: "接受答案数", key: "acceptAnswerNum",sortable: true},
        { title: "是否投票", key: "vote" },
        { title: "是否结束", key: "finish" },
        {
          title: "处理",
          key: "handle",
        //   options: ["delete"],
          button: [
            (h, params, vm) => {
              return h(
                "Poptip",
                {
                  props: {
                    confirm: true,
                    title: "你确定要删除吗?",
                  },
                  on: {
                    "on-ok": () => {
                      vm.$emit("on-delete", params);
                      vm.$emit(
                        "input",
                        params.tableData.filter(
                          (item, index) => index !== params.row.initRowIndex
                        )
                      );
                    },
                  },
                },
                [h("Button", "查看任务")]
              );
            },(h, params, vm) => {
              return h(
                "Poptip",
                {
                  props: {
                    confirm: true,
                    title: "你确定要删除吗?",
                  },
                  on: {
                    "on-ok": () => {
                      vm.$emit("on-delete", params);
                      vm.$emit(
                        "input",
                        params.tableData.filter(
                          (item, index) => index !== params.row.initRowIndex
                        )
                      );
                    },
                  },
                },
                [h("Button", "删除")]
              );
            },
          ],
        },
      ],
      tableData: [
          {"name":"abc","type":"sdsdds","publish":1,"totalAnswerNum":100,"vote":0,"finish":1}
      ],
    };
  },
  methods: {
    handleDelete(params) {
      console.log(params);
    },
    mounted() {
    //   getTableData().then((res) => {
    //     this.tableData = res.data;
    //   });
    },
  },
};
</script>
<style>
.task-page {
  text-align: center;
}
.qq-group-img {
  width: 100%;
}
.task-page-other-icon {
  width: 20px;
  vertical-align: middle;
  margin-right: 6px;
}
.task-page-other {
  text-align: left;
  margin: 8px;
}
.task-page-other .ivu-btn {
  margin-right: 6px;
}
</style>
