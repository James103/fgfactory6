<script setup>
    
    useHead({ title:'page_options' })

    definePageMeta({ layout:'home' })

    import { useAppStore } from '~/store/appStore.js'    
    const appStore = useAppStore()
    
    const { locale, locales, setLocale } = useI18n()

    const changeLocale = function(code) {
    
        setLocale(code)
        appStore.locale = code
    }

</script>

<template>

    <div class="container">
        <div class="row g-3">

            <div class="col-12">
                <div class="card">
                
                    <div class="card-header"><span class="text-white">{{ $t('options_about') }}</span></div>

                    <div class="card-body">
                        <div class="row gx-2 gy-3">

                            <div class="col-12">
                                <div class="row g-2">

                                    <div class="col-12">{{ $t('options_love') }}</div>

                                    <div class="col">
                                        <a href="https://www.patreon.com/bePatron?u=61283131" class="w-100 btn btn-secondary" target="_blank">
                                            <img src="/patreon.png" width="16" height="16" />
                                            <span class="ms-2 d-none d-sm-inline">{{ $t('options_patreon') }}</span>
                                        </a>
                                    </div>

                                    <div class="col">
                                        <a href="https://ko-fi.com/freddecgames" class="w-100 btn btn-secondary" target="_blank">
                                            <img src="/kofi.png" width="16" height="16" />
                                            <span class="ms-2 d-none d-sm-inline">{{ $t('options_kofi') }}</span>
                                        </a>
                                    </div>

                                    <form class="col" action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_blank">
                                        <input type="hidden" name="cmd" value="_s-xclick">
                                        <input type="hidden" name="hosted_button_id" value="7XYD7SJFKQ8M4">
                                        <button type="submit" class="w-100 btn btn-secondary">
                                            <img src="/paypal.png" width="16" height="16" />
                                            <span class="ms-2 d-none d-sm-inline">{{ $t('options_paypal') }}</span>
                                        </button>
                                    </form>

                                    <div class="col">
                                        <a href="https://discord.gg/ZXrggavUpv" class="w-100 btn btn-secondary" target="_blank">
                                            <img src="/discord.png" width="16" height="16" />
                                            <span class="ms-2 d-none d-sm-inline">{{ $t('options_discord') }}</span>
                                        </a>
                                    </div>

                                </div>
                            </div>

                            <div class="col-12">
								{{ $t('options_iconsBy') }}
								<a href="https://fontawesome.com/" target="_blank">Fontawesome</a>,
								<a href="https://www.flaticon.com/" target="_blank">Flaticon</a>,
								<a href="https://www.freepik.com/" target="_blank">Freepik</a>
							</div>

                            <div class="col-12">
								{{ $t('options_scenariosBy') }}
								<a href="https://www.satisfactorygame.com/" target="_blank">Satisfactory</a>
							</div>

                        </div>
                    </div>

                </div>
            </div>

            <div class="col-12">
                <div class="card">
                
                    <div class="card-header"><span class="text-white">{{ $t('options_language') }}</span></div>

                    <div class="card-body">
                        <div class="row g-2">
                            <div v-for="l in locales" :key="l.code" class="col-auto">
                                <button type="button" class="btn btn-secondary py-1" :class="{ 'text-bg-primary': locale == l.code }" @click="changeLocale(l.code)">
                                    <img :src="'/fgfactory/flags/' + l.code + '.png'" height="24">
                                </button>
                            </div>
                        </div>
                    </div>

                </div>
            </div>

            <div class="col-12">
                <div class="card">
                    <div class="card-header"><span class="text-white">{{ $t('options_localData') }}</span></div>
                    <div class="card-body">
                        <div class="row gx-3 gy-3">
                        
                            <div class="col-12 col-md-6">
                                <div class="row g-2">
                                
                                    <div class="col-12">
                                        <textarea id="localData" spellcheck="false" rows="3" class="w-100 form-control" disabled readonly>{{ appStore.localStorageData }}</textarea>
                                    </div>
                                    
                                    <div class="col-4">
                                        <button type="button" class="w-100 btn btn-danger px-0" @click="appStore.showModal('modalWipe');">
                                            <span><font-awesome-icon icon="fas fa-fw fa-skull" /></span>
                                            <span class="ms-2">{{ $t('options_wipeSave') }}</span>
                                        </button>
                                    </div>
                                    
                                    <div class="col-4">
                                        <button type="button" class="w-100 btn btn-secondary px-0" @click="appStore.exportAppState();">
                                            <span><font-awesome-icon icon="fas fa-fw fa-copy" /></span>
                                            <span class="ms-2">{{ $t('options_exportSave') }}</span>
                                        </button>
                                    </div>
                                    
                                    <div class="col-4">
                                        <button type="button" class="w-100 btn btn-secondary px-0" @click="appStore.downloadAppState();">
                                            <span><font-awesome-icon icon="fas fa-fw fa-download" /></span>
                                            <span class="ms-2">{{ $t('options_downloadSave') }}</span>
                                        </button>
                                    </div>
                                    
                                </div>
                            </div>

                            <div class="col-12 col-md-6">
                                <div class="row g-2">
                                
                                    <div class="col-12">
                                        <textarea spellcheck="false" rows="3" id="importData" class="w-100 form-control"></textarea>
                                    </div>
                                    
                                    <div class="col-4 ms-auto">
                                        <button type="button" class="w-100 btn btn-secondary px-0" @click="appStore.importAppState();">
                                            <span><font-awesome-icon icon="fas fa-fw fa-upload" /></span>
                                            <span class="ms-2">{{ $t('options_importSave') }}</span>
                                        </button>
                                    </div>
                                    
                                </div>
                            </div>
                        
                        </div>
                    </div>
                </div>
            </div>
        
        </div>
    </div>
    
    <div id="toast-container" class="toast-container position-fixed bottom-0 end-0 p-3">
        <toast-export />
        <toast-import-empty />
        <toast-import-corrupted />
    </div>
    
    <modal-wipe />

</template>
