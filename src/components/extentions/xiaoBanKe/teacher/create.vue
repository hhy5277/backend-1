<template>
  <div class="h-panel w-1200">
    <div class="h-panel-bar">
      <span class="h-panel-title">添加</span>
      <div class="h-panel-right">
        <Button color="primary" @click="create">添加</Button>
        <Button @click="$emit('close')" :text="true">取消</Button>
      </div>
    </div>
    <div class="h-panel-body">
      <Form mode="block" ref="form" :validOnChange="true" :showErrorTip="true" :rules="rules" :model="teacher">
        <Row :space="10">
          <Cell :width="6">
            <FormItem label="讲师名" prop="name">
              <input type="text" v-model="teacher.name" />
            </FormItem>
          </Cell>
          <Cell :width="18">
            <FormItem label="头像" prop="avatar">
              <image-upload v-model="teacher.avatar" name="头像"></image-upload>
            </FormItem>
          </Cell>
          <Cell :width="12">
            <FormItem label="邮箱" prop="username">
              <input type="text" v-model="teacher.username" />
            </FormItem>
          </Cell>
          <Cell :width="12">
            <FormItem label="密码" prop="password">
              <input type="text" v-model="teacher.password" />
            </FormItem>
          </Cell>
          <Cell :width="24">
            <FormItem label="简介" prop="short_desc">
              <textarea v-model="teacher.short_desc"></textarea>
            </FormItem>
          </Cell>
        </Row>
      </Form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      teacher: {
        name: '',
        avatar: '',
        short_desc: '',
        username: '',
        password: ''
      },
      rules: {
        required: ['name', 'avatar', 'short_desc', 'username', 'password']
      }
    };
  },
  methods: {
    create() {
      let validResult = this.$refs.form.valid();
      if (validResult.result) {
        R.Extentions.xiaoBanKe.Teacher.Store(this.teacher).then(resp => {
          this.$emit('success');
        });
      }
    }
  }
};
</script>
