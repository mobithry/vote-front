<script>
import VoteCandidate from "../VoteCandidate/index.vue";
export default {
  name: "Register",
  data() {
    return {
      user: {
        nationalCode: null,
        photo: null,
      },
      photoCaption: "تصویر را انتخاب کنید",
      message: null,
      isSubmitted: false,
      isAccepted: "allowed",
    };
  },
  methods: {
    handlePhoto(event) {
      this.user.photo = event.target.value;
      this.photoCaption = event.target.files[0].name;
    },
    submit() {
      if (this.user.nationalCode && this.user.photo) {
        this.isSubmitted = true;
      } else {
        this.message = "لطفا همه مقادیر را وارد کنید.";
      }
    },
  },
  components: { VoteCandidate },
};
</script>

<template>
  <div class="register">
    <template v-if="!isSubmitted">
      <h2 align="center">لطفا اطلاعات زیر را وارد کنید.</h2>
      <div>
        <label for="nationalCode">کد ملی: </label>
        <input
          v-model="user.nationalCode"
          type="number"
          name="nationalCode"
          id="nationalCode"
        />
      </div>
      <br />
      <div>
        <span>محل آپلو عکس : </span>
        <label class="register-file-label">
          {{ photoCaption }}
          <input
            type="file"
            id="photo"
            name="myfile"
            accept="image/*"
            @change="handlePhoto"
          />
        </label>
      </div>
      <br />
      <span class="register-note"
        >یک تصویر از چهره خود در حالی که کارت ملی و برگه ای که در آن متن زیر
        <br />را نوشته اید و امضا کردید و اثر انگشت خود را زده اید در دستتان است
        به<br />
        صورتی که متن نوشته و اطالعات کارت ملی و چهره کامال واضح باشد.
      </span>
      <br v-if="message" />
      <span v-if="message" class="register-error">{{ message }}</span>
      <br />
      <button class="register-submit" @click="submit">تایید</button>
    </template>
    <template v-else>
      <div class="register-sent" v-if="isAccepted == null && isSubmitted">
        اطلاعات هویتی شما در دست بررسی است لطفا تا احراز هویت منتظر بمانید.
      </div>
      <div
        class="register-denied"
        v-else-if="isAccepted == 'not allowed' && isSubmitted"
      >
        متاسفانه اطلاعات هویتی شما تایید نشد.
      </div>
      <VoteCandidate v-else/>
    </template>
  </div>
</template>

<style scoped lang="scss" src="./style.scss" />
