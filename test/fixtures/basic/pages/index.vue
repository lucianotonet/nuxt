<template>
  <div>
    <Head>
      <Title>Basic fixture</Title>
    </Head>
    <h1>Hello Nuxt 3!</h1>
    <div>RuntimeConfig | testConfig: {{ config.public.testConfig }}</div>
    <div>Composable | foo: {{ foo }}</div>
    <div>Composable | bar: {{ bar }}</div>
    <div>Composable | template: {{ templateAutoImport }}</div>
    <div>Composable | star: {{ useNestedBar() }}</div>
    <DevOnly>Some dev-only info</DevOnly>
    <div><DevOnly>Some dev-only info</DevOnly></div>
    <div>Path: {{ $route.fullPath }}</div>
    <NuxtLink to="/">
      Link
    </NuxtLink>
    <NuxtLink to="/chunk-error" :prefetch="false">
      Chunk error
    </NuxtLink>
    Some value: {{ someValue }}
    <button @click="someValue++">
      Increment state
    </button>
    <NuxtLink to="/no-scripts">
      to no script
    </NuxtLink>
    <NestedSugarCounter :multiplier="2" />
    <CustomComponent />
    <Spin>Test</Spin>
    <component :is="`test${'-'.toString()}global`" />
    <component :is="`with${'-'.toString()}suffix`" />
    <ClientWrapped ref="clientRef" style="color: red;" class="client-only" />
    <ServerOnlyComponent class="server-only" style="background-color: gray;" />
  </div>
</template>

<script setup lang="ts">
import { setupDevtoolsPlugin } from '@vue/devtools-api'
import { useRuntimeConfig } from '#imports'
import { importedRE, importedValue } from '~/some-exports'

setupDevtoolsPlugin({}, () => {}) as any

const config = useRuntimeConfig()

const someValue = useState('val', () => 1)

definePageMeta({
  alias: '/some-alias',
  other: ref('test'),
  imported: importedValue,
  something: importedRE.test('an imported regex')
})

// reset title template example
useHead({
  titleTemplate: ''
})

const foo = useFoo()
const bar = useBar()
const clientRef = ref()

onMounted(() => {
  clientRef.value.exposedFunc()
})
</script>
