<script lang="ts">
  import classNames from 'classnames';
  import { getContext } from 'svelte';
  import type { ButtonType } from '../types';

  const group = getContext('group');

  export let pill = false;
  export let outline = false;
  export let gradient = false;
  export let size: 'xs' | 'sm' | 'md' | 'lg' | 'xl' = group ? 'sm' : 'md';
  export let href: string | undefined = undefined;
  export let btnClass: string | undefined = undefined;
  export let type: ButtonType = 'button';
  export let color: Color | Gradient = group ? (outline ? 'dark' : 'alternative') : 'blue';
  export let shadow: Color | null = null;

  type Color =
    | 'blue'
    | 'cyan'
    | 'lime'
    | 'green'
    | 'pink'
    | 'red'
    | 'teal'
    | 'yellow'
    | 'purple'
    | 'light'
    | 'dark'
    | 'primary'
    | 'alternative';
  type Gradient =
    | 'purpleToBlue'
    | 'cyanToBlue'
    | 'greenToBlue'
    | 'purpleToPink'
    | 'pinkToOrange'
    | 'tealToLime'
    | 'redToYellow';

  const colorClasses: Partial<Record<Color, string>> = {
    blue: 'text-white bg-blue-700 hover:bg-blue-800 focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800',
    dark: 'text-white bg-gray-800 hover:bg-gray-900 focus:ring-gray-300 dark:bg-gray-800 dark:hover:bg-gray-700 dark:focus:ring-gray-700',
    alternative:
      'text-gray-900 bg-white border border-gray-200 dark:border-gray-600 hover:bg-gray-100 focus:ring-gray-200 dark:bg-gray-800 dark:text-gray-400 hover:text-blue-700 focus:text-blue-700 dark:focus:text-white dark:hover:text-white dark:hover:bg-gray-700 dark:focus:ring-gray-700',
    light:
      'text-gray-900 bg-white border border-gray-300 hover:bg-gray-100 focus:ring-gray-200 dark:bg-gray-800 dark:text-white dark:border-gray-600 dark:hover:bg-gray-700 dark:hover:border-gray-600 dark:focus:ring-gray-700',
    green:
      'text-white bg-green-700 hover:bg-green-800 focus:ring-green-300 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800',
    red: 'text-white bg-red-700 hover:bg-red-800 focus:ring-red-300 dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-900',
    yellow: 'text-white bg-yellow-400 hover:bg-yellow-500 focus:ring-yellow-300 dark:focus:ring-yellow-900',
    primary:
      'text-white bg-primary-700 hover:bg-primary-800 focus:ring-primary-300 dark:bg-primary-600 dark:hover:bg-primary-700 dark:focus:ring-primary-800',
    purple:
      'text-white bg-purple-700 hover:bg-purple-800 focus:ring-purple-300 dark:bg-purple-600 dark:hover:bg-purple-700 dark:focus:ring-purple-900'
  };

  const gradientClasses: Partial<Record<Color | Gradient, string>> = {
    blue: 'text-white bg-dbl-gradient-to-br bg-200% from-blue-500 via-blue-600 to-blue-700 hover:bg-right-bottom bg-200% focus:ring-blue-300 dark:focus:ring-blue-800 ',
    green:
      'text-white bg-dbl-gradient-to-br bg-200% from-green-400 via-green-500 to-green-600 hover:bg-right-bottom bg-200% focus:ring-green-300 dark:focus:ring-green-800',
    cyan: 'text-white bg-dbl-gradient-to-br bg-200% from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-right-bottom bg-200% focus:ring-cyan-300 dark:focus:ring-cyan-800',
    teal: 'text-white bg-dbl-gradient-to-br bg-200% from-teal-400 via-teal-500 to-teal-600 hover:bg-right-bottom bg-200% focus:ring-teal-300 dark:focus:ring-teal-800',
    lime: 'text-gray-900 bg-dbl-gradient-to-br bg-200% from-lime-200 via-lime-400 to-lime-500 hover:bg-right-bottom bg-200% focus:ring-lime-300 dark:focus:ring-lime-800',
    red: 'text-white bg-dbl-gradient-to-br bg-200% from-red-400 via-red-500 to-red-600 hover:bg-right-bottom bg-200% focus:ring-red-300 dark:focus:ring-red-800',
    pink: 'text-white bg-dbl-gradient-to-br bg-200% from-pink-400 via-pink-500 to-pink-600 hover:bg-right-bottom bg-200% focus:ring-pink-300 dark:focus:ring-pink-800',
    purple:
      'text-white bg-dbl-gradient-to-br bg-200% from-purple-500 via-purple-600 to-purple-700 hover:bg-right-bottom bg-200% focus:ring-purple-300 dark:focus:ring-purple-800',
    purpleToBlue:
      'text-white bg-dbl-gradient-to-br bg-200% from-purple-600 to-blue-500 hover:bg-right-bottom focus:ring-blue-300 dark:focus:ring-blue-800',
    cyanToBlue:
      'text-white bg-dbl-gradient-to-br bg-200% from-cyan-500 to-blue-500 hover:bg-right-bottom focus:ring-cyan-300 dark:focus:ring-cyan-800',
    greenToBlue:
      'text-white bg-dbl-gradient-to-br bg-200% from-green-400 to-blue-600 hover:bg-right-bottom focus:ring-green-200 dark:focus:ring-green-800',
    purpleToPink:
      'text-white bg-dbl-gradient-to-br bg-200% from-purple-500 to-pink-500 hover:bg-right-bottom focus:ring-purple-200 dark:focus:ring-purple-800',
    pinkToOrange:
      'text-white bg-dbl-gradient-to-br bg-200% from-pink-500 to-orange-400 hover:bg-right-bottom focus:ring-pink-200 dark:focus:ring-pink-800',
    tealToLime:
      'text-gray-900 bg-dbl-gradient-to-br bg-200% from-teal-200 to-lime-200 hover:bg-right-bottom focus:ring-lime-200 dark:focus:ring-teal-700',
    redToYellow:
      'text-gray-900 bg-dbl-gradient-to-br bg-200% from-red-200 via-red-300 to-yellow-200 hover:bg-right-bottom focus:ring-red-100 dark:focus:ring-red-400'
  };

  const coloredShadowClasses: Partial<Record<Color, string>> = {
    blue: 'shadow-lg shadow-blue-500/50 dark:shadow-lg dark:shadow-blue-800/80',
    green: 'shadow-lg shadow-green-500/50 dark:shadow-lg dark:shadow-green-800/80',
    cyan: 'shadow-lg shadow-cyan-500/50 dark:shadow-lg dark:shadow-cyan-800/80',
    teal: 'shadow-lg shadow-teal-500/50 dark:shadow-lg dark:shadow-teal-800/80 ',
    lime: 'shadow-lg shadow-lime-500/50 dark:shadow-lg dark:shadow-lime-800/80',
    red: 'shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 ',
    pink: 'shadow-lg shadow-pink-500/50 dark:shadow-lg dark:shadow-pink-800/80',
    purple: 'shadow-lg shadow-purple-500/50 dark:shadow-lg dark:shadow-purple-800/80'
  };

  const outlineClasses: Partial<Record<Color, string>> = {
    blue: 'text-blue-700 hover:text-white border border-blue-700 hover:bg-blue-800 focus:ring-blue-300 dark:border-blue-500 dark:text-blue-500 dark:hover:text-white dark:hover:bg-blue-600 dark:focus:ring-blue-800',
    light:
      'text-gray-500 hover:text-gray-900 bg-white border border-gray-200 dark:border-gray-600 dark:hover:text-white dark:text-gray-400 hover:bg-gray-50 dark:bg-gray-700 dark:hover:bg-gray-600 focus:ring-4 focus:ring-gray-300 dark:focus:ring-gray-400',
    dark: 'text-gray-900 hover:text-white border border-gray-800 hover:bg-gray-900 focus:bg-gray-900 focus:text-white focus:ring-gray-300 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-gray-800',
    green:
      'text-green-700 hover:text-white border border-green-700 hover:bg-green-800 focus:ring-green-300 dark:border-green-500 dark:text-green-500 dark:hover:text-white dark:hover:bg-green-600 dark:focus:ring-green-800',
    red: 'text-red-700 hover:text-white border border-red-700 hover:bg-red-800 focus:ring-red-300 dark:border-red-500 dark:text-red-500 dark:hover:text-white dark:hover:bg-red-600 dark:focus:ring-red-900',
    yellow:
      'text-yellow-400 hover:text-white border border-yellow-400 hover:bg-yellow-500 focus:ring-yellow-300 dark:border-yellow-300 dark:text-yellow-300 dark:hover:text-white dark:hover:bg-yellow-400 dark:focus:ring-yellow-900',
    purple:
      'text-purple-700 hover:text-white border border-purple-700 hover:bg-purple-800 focus:ring-purple-300 dark:border-purple-400 dark:text-purple-400 dark:hover:text-white dark:hover:bg-purple-500 dark:focus:ring-purple-900'
  };

  const sizeClasses = {
    xs: 'px-3 py-2 text-xs',
    sm: 'px-4 py-2 text-sm',
    md: 'px-5 py-2.5 text-sm',
    lg: 'px-5 py-3 text-base',
    xl: 'px-6 py-3.5 text-base'
  };

  function rounded(gradientOutline = false) {
    if (group) {
      return pill
        ? 'first:rounded-l-full last:rounded-r-full'
        : gradientOutline
        ? 'first:rounded-l-md last:rounded-r-md'
        : 'first:rounded-l-lg last:rounded-r-lg';
    }
    return pill ? 'rounded-full' : gradientOutline ? 'rounded-md' : 'rounded-lg';
  }

  const hasBorder = () => outline || color === 'alternative' || color === 'light';

  let buttonClass: string;
  $: buttonClass = btnClass
    ? btnClass
    : classNames(
        'text-center font-medium',
        group ? 'focus:ring-2' : 'focus:ring-4',
        group && 'focus:z-10',
        group || 'focus:outline-none',
        outline && gradient ? 'p-0.5' : 'inline-flex items-center justify-center ' + sizeClasses[size],
        gradient
          ? gradientClasses[color]
          : outline
          ? outlineClasses[color as Color]
          : colorClasses[color as Color],
        color === 'alternative' &&
          (group
            ? 'dark:bg-gray-700 dark:text-white dark:border-gray-700 dark:hover:border-gray-600 dark:hover:bg-gray-600'
            : 'dark:bg-transparent dark:border-gray-800 dark:hover:border-gray-700'),
        outline &&
          color === 'dark' &&
          (group ? 'dark:text-white dark:border-white' : 'dark:text-gray-400 dark:border-gray-700'),
        hasBorder() && group && 'border-l-0 first:border-l',
        rounded(false),
        shadow && coloredShadowClasses[shadow],
        'transition-all',
        $$props.disabled && 'cursor-not-allowed opacity-50',
        $$props.class
      );

  let gradientOutlineClass: string;
  $: gradientOutlineClass = classNames(
    'inline-flex items-center justify-center',
    sizeClasses[size],
    rounded(true),
    'bg-white text-gray-900 dark:bg-gray-900 dark:text-white', // this is limitation - no transparency
    'group-hover:bg-opacity-0 group-hover:text-inherit'
  );
</script>

<svelte:element
  this={href ? 'a' : 'button'}
  type={href ? undefined : type}
  {href}
  {...$$restProps}
  class={buttonClass}
  on:click
  on:change
  on:keydown
  on:keyup
  on:mouseenter
  on:mouseleave>
  {#if outline && gradient}
    <!-- Trick to prentend outline without using border
		This has a limitation of no supporting transparency as
		background is set to bg-white dark:bg-gray-900 -->
    <span class={gradientOutlineClass}><slot /></span>
  {:else}
    <slot />
  {/if}
</svelte:element>
