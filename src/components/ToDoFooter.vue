<template>
  <div id="alert-border-1" role="alert" class="my-alert">
    <svg xmlns="http://www.w3.org/2000/svg" width="26" height="26" viewBox="0 0 26 26" fill="none">
      <path
        d="M13 19.25C13.3542 19.25 13.6513 19.13 13.8913 18.89C14.1313 18.65 14.2508 18.3533 14.25 18C14.25 17.6458 14.13 17.3487 13.89 17.1087C13.65 16.8687 13.3533 16.7492 13 16.75C12.6458 16.75 12.3487 16.87 12.1087 17.11C11.8687 17.35 11.7492 17.6467 11.75 18C11.75 18.3542 11.87 18.6512 12.11 18.8912C12.35 19.1312 12.6467 19.2508 13 19.25ZM11.75 14.25H14.25V6.75H11.75V14.25ZM13 25.5C11.2708 25.5 9.64583 25.1717 8.125 24.515C6.60417 23.8583 5.28125 22.9679 4.15625 21.8438C3.03125 20.7188 2.14083 19.3958 1.485 17.875C0.829167 16.3542 0.500833 14.7292 0.5 13C0.5 11.2708 0.828333 9.64583 1.485 8.125C2.14167 6.60417 3.03208 5.28125 4.15625 4.15625C5.28125 3.03125 6.60417 2.14083 8.125 1.485C9.64583 0.829167 11.2708 0.500833 13 0.5C14.7292 0.5 16.3542 0.828333 17.875 1.485C19.3958 2.14167 20.7188 3.03208 21.8438 4.15625C22.9688 5.28125 23.8596 6.60417 24.5162 8.125C25.1729 9.64583 25.5008 11.2708 25.5 13C25.5 14.7292 25.1717 16.3542 24.515 17.875C23.8583 19.3958 22.9679 20.7188 21.8438 21.8438C20.7188 22.9688 19.3958 23.8596 17.875 24.5162C16.3542 25.1729 14.7292 25.5008 13 25.5ZM13 23C15.7917 23 18.1562 22.0312 20.0938 20.0938C22.0312 18.1562 23 15.7917 23 13C23 10.2083 22.0312 7.84375 20.0938 5.90625C18.1562 3.96875 15.7917 3 13 3C10.2083 3 7.84375 3.96875 5.90625 5.90625C3.96875 7.84375 3 10.2083 3 13C3 15.7917 3.96875 18.1562 5.90625 20.0938C7.84375 22.0312 10.2083 23 13 23Z"
        fill="#6348fe"
      />
    </svg>
    <div>{{ listSummary }}</div>
  </div>

  <div class="btn-group">
    <button class="btn" type="submit">Clear Completed</button>
    <button class="btn" type="submit">Clear All</button>
  </div>
</template>

<script>
import '../assets/reset.css'

export default {
  name: 'ToDoFooter',
  props: {
    listSummary: {
      type: String
    }
  }
}
</script>

<style scoped>
div.my-alert {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: var(--tw-size-4);
  margin-bottom: var(--tw-size-4);
  --tw-text-opacity: 1;
  color: #6348fe;
  border-top-width: 0.4rem;
  --tw-border-opacity: 1;
  border-color: #6348fe;
  --tw-bg-opacity: 1;
  background-color: rgb(var(--tw-color-blue-50) / var(--tw-bg-opacity));
}

:is(.dark div.my-alert) {
  --tw-text-opacity: 1;
  color: rgb(var(--tw-color-blue-400) / var(--tw-text-opacity));
  --tw-bg-opacity: 1;
  background-color: rgb(var(--tw-color-gray-800) / var(--tw-bg-opacity));
  --tw-border-opacity: 1;
  border-color: rgb(var(--tw-color-blue-800) / var(--tw-border-opacity));
}

div.my-alert > svg {
  flex-shrink: 0;
  width: var(--tw-size-6);
  height: var(--tw-size-6);
}

div.my-alert > div {
  -webkit-margin-start: var(--tw-size-3);
  margin-inline-start: var(--tw-size-3);
  font-size: var(--tw-font-size-lg);
  line-height: var(--tw-line-height-5);
  font-weight: var(--tw-font-weight-medium);
}

@media screen and (min-width: 620px) {
  div.my-alert {
    width: 70%;
  }
  div.my-alert > svg {
    width: var(--tw-size-8);
    height: var(--tw--size-8);
  }
  div.my-alert > div {
    font-size: var(--tw-font-size-2xl);
  }
}
</style>
