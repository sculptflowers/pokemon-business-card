<script lang="ts">
    import type { CardData } from './types';
    import EditableField from '$lib/EditableField.svelte';
    import gamefreakLogo from '$lib/assets/gamefreakLogo.svg';
    import { onMount } from 'svelte';

    interface Props {
        data: CardData;
        onUpdate: (field: keyof CardData, value: string) => void;
        cardRef?: HTMLDivElement;
    }

    // $bindable() allows parent to do bind:cardRef (replaces forwardRef)
    let { data, onUpdate, cardRef = $bindable() }: Props = $props();

    const monModules = import.meta.glob('./assets/mons/*.png', { eager: true, query: '?url', import: 'default' });
    const monPaths = Object.values(monModules) as string[];
    
    let mon = $state(monPaths[0]);

    onMount(() => {
        if (monPaths.length > 0) {
            mon = monPaths[Math.floor(Math.random() * monPaths.length)];
        }
    });
</script>

<div
        bind:this={cardRef}
        class="bg-white relative w-[1071px] h-[646px] font-display pt-8 pl-4 pr-4 pb-12 shadow-xl"
>
    <!-- Logo top area -->
    <div class="flex items-center w-[510px]">
        <img
                src={gamefreakLogo}
                alt="Logo"
                class="w-[510px] object-contain"
                crossorigin="anonymous"
        />
    </div>

    <!-- Main content area -->
    <div class="absolute bottom-[80px] left-[108px] flex gap-10 w-[962px] h-[359px]">
        <!-- Mon -->
        <img
                src={mon}
                alt="Mon"
                crossorigin="anonymous"
        />

        <!-- Info section -->
        <div class="flex-1 flex flex-col">

            <!-- Department + Position -->
            <div class="flex font-A inline-flex">
                <EditableField
                        value={data.department}
                        className="font-A"
                        onChange={(v) => onUpdate('department', v)}
                />
                <EditableField
                        value={data.position}
                        className="font-A"
                        onChange={(v) => onUpdate('position', v)}
                />
            </div>

            <!-- Name JPN -->
            <EditableField
                    value={data.nameJpn}
                    className="-mt-[24px] font-B  leading-0"
                    onChange={(v) => onUpdate('nameJpn', v)}
            />

            <!-- Separator lines -->
            <div class="-mt-[30px]">
                <div class="h-[2px] bg-[#AEAEB2]"></div>
                <div class="h-[4px] bg-[#8E8E93] mt-[2px]"></div>
            </div>

            <!-- Sub name -->
            <EditableField
                    value={data.subName}
                    className="font-C tracking-wide"
                    onChange={(v) => onUpdate('subName', v)}
            />

            <!-- Company -->
            <EditableField
                    value={data.company}
                    className="font-D  leading-tight"
                    onChange={(v) => onUpdate('company', v)}
            />

            <!-- ZIP -->
            <div class="flex items-center -mt-[16px] font-A text-[24px]  leading-tight">
                <span class="mr-0.5">ZIP:</span>
                <EditableField
                        value={data.zip}
                        className="font-A text-[24px]"
                        onChange={(v) => onUpdate('zip', v)}
                />
            </div>

            <!-- Address -->
            <EditableField
                    value={data.address}
                    className="-mt-[16px] font-A text-[24px] "
                    onChange={(v) => onUpdate('address', v)}
            />

            <!-- TEL / FAX -->
            <div class="flex gap-[154px] -mt-[12px] font-A text-[20px] ">
                <div class="flex items-center">
                    <span class="mr-0.5">TEL:</span>
                    <EditableField
                            value={data.tel}
                            className="font-A text-[16px]"
                            onChange={(v) => onUpdate('tel', v)}
                    />
                </div>
                <div class="flex items-center">
                    <span class="mr-0.5">FAX:</span>
                    <EditableField
                            value={data.fax}
                            className="font-A text-[16px]"
                            onChange={(v) => onUpdate('fax', v)}
                    />
                </div>
            </div>

            <!-- Email -->
            <div class="flex items-center -mt-[10px] font-A text-[24px]  gap-2">
              <span class="whitespace-nowrap flex-shrink-0"> E-Mail: </span>

                <EditableField
                        value={data.email}
                        className="font-A text-[18px] w-full"
                        onChange={(v) => onUpdate('email', v)}
                />
            </div>

            <!-- Website -->
            <EditableField
                    value={data.website}
                    className="-mt-[16px] font-A text-[24px] "
                    onChange={(v) => onUpdate('website', v)}
            />

        </div>
    </div>
</div>