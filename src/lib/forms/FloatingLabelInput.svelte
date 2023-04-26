<script lang="ts">
  import classNames from 'classnames';
  import generateId from '../utils/generateId.js';
  import type { InputType } from '../types';

  export let id: string = generateId();
  export let style: 'filled' | 'outlined' | 'standard' = 'standard';
  export let type: InputType = 'text';
  export let size: 'small' | 'default' = 'default';
  export let color: 'base' | 'green' | 'red' = 'base';
  export let value = '';
  export let label = '';

  const divClasses = {
    filled: 'relative rounded-t-lg bg-gray-50 dark:bg-gray-700 border-0 border-b-2',
    outlined: 'relative border rounded-lg',
    standard: 'relative z-0 border-0 border-b-2'
  };

  const inputSizes = {
    filled: {
      small: 'px-2.5 pb-1.5 pt-4',
      default: 'px-2.5 pb-2.5 pt-5'
    },
    outlined: {
      small: 'px-2.5 pb-1.5 pt-3',
      default: 'px-2.5 pb-2.5 pt-4'
    },
    standard: {
      small: 'px-2.5 py-2',
      default: 'px-2.5 py-2.5'
    }
  };

  const labelSizes = {
    filled: {
      small: 'top-3',
      default: 'top-4'
    },
    outlined: {
      small: 'top-1',
      default: 'top-2'
    },
    standard: {
      small: 'top-3',
      default: 'top-3'
    }
  };

  const inputClasses = {
    filled:
      'block w-full text-sm text-gray-900 bg-transparent border-0 appearance-none dark:text-white focus:outline-none focus:ring-0 peer',
    outlined:
      'block w-full text-sm text-gray-900 bg-transparent border-0 appearance-none dark:text-white focus:outline-none focus:ring-0 peer',
    standard:
      'block w-full text-sm text-gray-900 bg-transparent border-0 appearance-none dark:text-white focus:outline-none focus:ring-0 peer'
  };

  const labelClasses = {
    filled:
      'absolute pointer-events-none text-sm duration-300 transform -translate-y-4 scale-75 z-10 origin-[0] ml-2.5 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-4',
    outlined:
      'absolute pointer-events-none text-sm duration-300 transform -translate-y-5 scale-75 z-10 origin-[0] ml-1.5 px-1 bg-white dark:bg-gray-900 px-1 peer-placeholder-shown:scale-100 peer-placeholder-shown:-translate-y-1/2 peer-placeholder-shown:top-1/2 peer-focus:top-2 peer-focus:scale-75 peer-focus:-translate-y-5 peer-placeholder-shown:bg-none',
    standard:
      'absolute pointer-events-none text-sm duration-300 transform -translate-y-6 scale-75 -z-10 origin-[0] ml-2.5 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6'
  };

  const inputColorClasses = {
    base: 'border-gray-300 dark:border-gray-600 dark:focus-within:border-blue-500 focus-within:border-blue-600',
    green:
      'border-green-600 dark:border-green-500 dark:focus-within:border-green-500 focus-within:border-green-600',
    red: 'border-red-600 dark:border-red-500 dark:focus-within:border-red-500 focus-within:border-red-600'
  };

  const labelColorClasses = {
    base: 'text-gray-500 dark:text-gray-400 peer-focus:text-blue-600 peer-focus:dark:text-blue-500',
    green: 'text-green-600 dark:text-green-500',
    red: 'text-red-600 dark:text-red-500'
  };

  const leftPadding = { small: 'pl-9', default: 'pl-10' };
  const rightPadding = { small: 'pr-9', default: 'pr-10' };

  // you need to this to avoid 2-way binding
  function setType(node: HTMLInputElement, _type: string) {
    node.type = _type;
    return {
      update(_type: string) {
        node.type = _type;
      }
    };
  }

  let floatClass = 'flex absolute inset-y-0 items-center text-gray-500 dark:text-gray-400';
</script>

<div
  class={classNames(
    divClasses[style],
    inputColorClasses[color],
    $$slots.left && leftPadding[size],
    $$slots.right && rightPadding[size]
  )}>
  {#if $$slots.left}
    <div class="{floatClass} left-0 pl-2.5 pointer-events-none"><slot name="left" /></div>
  {/if}
  <input
    {id}
    {...$$restProps}
    bind:value
    on:blur
    on:change
    on:click
    on:focus
    on:input
    on:keydown
    on:keypress
    on:keyup
    on:mouseenter
    on:mouseleave
    on:mouseover
    on:paste
    use:setType={type}
    placeholder=" "
    class={classNames(inputClasses[style], inputSizes[style][size], $$props.class)} />
  {#if $$slots.right}
    <div class="{floatClass} right-0 pr-2.5"><slot name="right" /></div>
  {/if}

  <label
    for={id}
    class={classNames(
      labelClasses[style],
      labelColorClasses[color],
      labelSizes[style][size],
      $$props.labelClass
    )}>
    {label}
  </label>
</div>
