<template>
  <q-btn color="primary-dark" :label="$t('repositories.new_repository.heading')" @click="dialog = true" />

  <q-dialog v-model="dialog" @hide="resetForm">
    <q-card style="width: 500px">
      <q-card-section class="flex justify-between">
        <h2 class="text-h6 q-my-none">
          {{ $t('repositories.new_repository.heading') }}
        </h2>
        <q-btn v-close-popup icon="close" flat round dense />
      </q-card-section>

      <q-separator />

      <q-form @submit="createRepository">
        <q-card-section>
          <q-input v-model="repository.repository"
                   :label="$t('repositories.new_repository.form.name.label')"
                   class="q-mb-sm"
                   name="name"
                   autocomplete="off"
                   autofocus
                   required />

          <q-input v-model="repository.body.type"
                   :label="$t('repositories.new_repository.form.type.label')"
                   class="q-mb-sm"
                   name="type"
                   disable />

          <q-input v-model="repository.body.settings.location"
                   :label="$t('repositories.new_repository.form.location.label')"
                   class="q-mb-sm"
                   name="location"
                   required />

          <q-input v-model="repository.body.settings.chunkSize"
                   :label="$t('repositories.new_repository.form.chunk_size.label')"
                   class="q-mb-sm"
                   name="chunkSize" />

          <q-input v-model="repository.body.settings.maxRestoreBytesPerSec"
                   :label="$t('repositories.new_repository.form.max_restore_bytes_per_sec.label')"
                   class="q-mb-sm"
                   name="maxRestoreBytesPerSec"
                   required />

          <q-input v-model="repository.body.settings.maxSnapshotBytesPerSec"
                   :label="$t('repositories.new_repository.form.max_snapshot_bytes_per_sec.label')"
                   class="q-mb-sm"
                   name="maxSnapshotBytesPerSec"
                   required />

          <div class="q-mt-md">
            <q-checkbox v-model="repository.body.settings.compress"
                        :label="$t('repositories.new_repository.form.compress.label')"
                        class="q-mb-sm"
                        name="compress" />
          </div>

          <div>
            <q-checkbox v-model="repository.body.settings.readonly"
                        :label="$t('repositories.new_repository.form.readonly.label')"
                        name="readonly" />
          </div>
        </q-card-section>

        <q-card-section>
          <q-btn :disable="requestState.loading || !formValid"
                 :loading="requestState.loading"
                 :label="$t('defaults.create')"
                 color="positive"
                 type="submit"
                 class="q-mr-md" />
          <q-btn v-close-popup flat :label="$t('defaults.close')" />
        </q-card-section>
      </q-form>
    </q-card>
  </q-dialog>
</template>

<script setup lang="ts">
  import { useNewSnapshotRepository } from '../../composables/components/repositories/NewSnapshotRepository'

  const emit = defineEmits(['reload'])
  const {
    repository,
    requestState,
    dialog,
    formValid,
    resetForm,
    createRepository
  } = useNewSnapshotRepository({ emit })
</script>