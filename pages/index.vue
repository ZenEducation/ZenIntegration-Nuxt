<template>
  <Form/>
</template>

<script>
import Form from '../components/Form.vue';
import awsconfig from '../src/aws-exports';
import { Amplify, Auth } from "aws-amplify";

Amplify.configure(awsconfig);

export default {
    name: 'IndexPage',
    components: { Form }
}
</script>
