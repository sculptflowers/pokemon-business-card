<script lang="ts">
    interface Props {
        value?: string;
        className?: string;
        onChange?: (value: string) => void;
    }

    let { value = '', className = '', onChange }: Props = $props();

    function handleInput(e: Event) {
        onChange?.((e.target as HTMLInputElement).value);
    }

    function handleKeydown(e: KeyboardEvent) {
        if (e.key === 'Enter') (e.target as HTMLInputElement).blur();
    }
</script>

<input
        type="text"
        {value}
        oninput={handleInput}
        onkeydown={handleKeydown}
        class="    bg-transparent
    leading-none
    p-0 m-0
    outline-none

    border-b border-transparent

    hover:border-gray-300
    focus:border-b-gray-600

    hover:bg-gray-50
    focus:bg-gray-100
    focus:rounded-sm

    transition-all duration-150 min-w-0 w-full {className}"
/>