import { JSX } from "solid-js";
//#region src/states/create-select-state.d.ts
interface SelectStateProperties<T> {
  isSelected: (value: T) => boolean;
  select: (value: T) => void;
  hasSelected: () => boolean;
  isActive: (value: T) => boolean;
  hasActive: () => boolean;
  focus: (value: T) => void;
  blur: () => void;
  disabled: () => boolean;
}
interface SingleSelectStateControlledOptions<T> {
  multiple?: false;
  toggleable?: boolean;
  /** `undefined` means nothing is selected, which is also what `toggleable` produces. */
  value: T | undefined;
  onChange?: (value?: T) => void;
  disabled?: boolean;
  by?: (a: T, b: T) => boolean;
}
interface SingleSelectStateUncontrolledOptions<T> {
  multiple?: false;
  toggleable?: boolean;
  /** `undefined` starts with nothing selected. */
  defaultValue: T | undefined;
  onChange?: (value?: T) => void;
  disabled?: boolean;
  by?: (a: T, b: T) => boolean;
}
type SingleSelectStateOptions<T> = SingleSelectStateControlledOptions<T> | SingleSelectStateUncontrolledOptions<T>;
/**
 * Creates a selection state that holds at most one value, and tracks which
 * value is active. Backs `Accordion`, `Select`, `Listbox`, `RadioGroup` and
 * `TabGroup`.
 *
 * Pass `by` when the values are objects, since the default comparison is by
 * reference.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#select-state}
 */
export declare function createSingleSelectState<T>(options: SingleSelectStateOptions<T>): SelectStateProperties<T>;
interface MultipleSelectStateControlledOptions<T> {
  multiple: true;
  toggleable?: boolean;
  value: T[];
  onChange?: (value: T[]) => void;
  disabled?: boolean;
  by?: (a: T, b: T) => boolean;
}
interface MultipleSelectStateUncontrolledOptions<T> {
  multiple: true;
  toggleable?: boolean;
  defaultValue: T[];
  onChange?: (value: T[]) => void;
  disabled?: boolean;
  by?: (a: T, b: T) => boolean;
}
type MultipleSelectStateOptions<T> = MultipleSelectStateControlledOptions<T> | MultipleSelectStateUncontrolledOptions<T>;
/**
 * Creates a selection state that holds an array of values, and tracks which
 * value is active. Requires `multiple: true`.
 *
 * Pass `by` when the values are objects, since the default comparison is by
 * reference.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#select-state}
 */
export declare function createMultipleSelectState<T>(options: MultipleSelectStateOptions<T>): SelectStateProperties<T>;
interface SelectStateRenderProps<T> {
  children?: JSX.Element | ((state: SelectStateProperties<T>) => JSX.Element);
}
/**
 * Reads the nearest select state from context. Throws when there is none.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#select-state}
 */
export declare function useSelectState<T>(): SelectStateProperties<T>;
/**
 * Passes the nearest select state to a render prop. A function child is
 * treated as a render prop only when it declares exactly one parameter.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#select-state}
 */
export declare function SelectStateChild<T>(props: SelectStateRenderProps<T>): JSX.Element;
//#endregion
//#region src/utils/types.d.ts
type Prettify<T> = { [K in keyof T]: T[K]; } & {};
type OmitAndMerge<A, B> = A & Omit<B, keyof A>;
//#endregion
//#region src/utils/dynamic-prop.d.ts
type ValidElements = keyof JSX.IntrinsicElements;
type ValidComponent<P> = (props: P) => JSX.Element;
type ValidConstructor = ValidElements | ValidComponent<any> | (string & {});
type DynamicProps<T extends ValidConstructor> = T extends ValidElements ? JSX.IntrinsicElements[T] : T extends ValidComponent<infer U> ? U : Record<string, unknown>;
type UnboxIntrinsicElements<T> = T extends JSX.HTMLAttributes<infer U> ? U : never;
type RefCallback<T> = (el: T) => void;
type RefField<T> = T | RefCallback<T>;
type UnboxComponentProp<U> = U extends {
  ref: infer X;
} ? X : never;
type DynamicNode<T extends ValidConstructor> = T extends ValidElements ? UnboxIntrinsicElements<JSX.IntrinsicElements[T]> : T extends ValidComponent<infer U> ? UnboxComponentProp<U> : never;
interface WithRef<T extends ValidConstructor> {
  ref?: RefField<DynamicNode<T>>;
}
interface DynamicComponent<T extends ValidConstructor> {
  as?: T;
}
interface DynamicComponentWithRef<T extends ValidConstructor> extends WithRef<T> {
  as?: T;
}
type HeadlessProps<T extends ValidConstructor, V = unknown> = OmitAndMerge<V & DynamicComponent<T>, DynamicProps<T>>;
type HeadlessPropsWithRef<T extends ValidConstructor, V = unknown> = OmitAndMerge<V & DynamicComponentWithRef<T>, DynamicProps<T>>;
//#endregion
//#region src/components/accordion/Accordion.d.ts
export type AccordionSingleControlledBaseProps<V> = Prettify<SingleSelectStateControlledOptions<V> & SelectStateRenderProps<V>>;
export type AccordionSingleControlledProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, AccordionSingleControlledBaseProps<V>>;
export type AccordionSingleUncontrolledBaseProps<V> = Prettify<SingleSelectStateUncontrolledOptions<V> & SelectStateRenderProps<V>>;
export type AccordionSingleUncontrolledProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, AccordionSingleUncontrolledBaseProps<V>>;
export type AccordionMultipleControlledBaseProps<V> = Prettify<MultipleSelectStateControlledOptions<V> & SelectStateRenderProps<V>>;
export type AccordionMultipleControlledProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, AccordionMultipleControlledBaseProps<V>>;
export type AccordionMultipleUncontrolledBaseProps<V> = Prettify<MultipleSelectStateUncontrolledOptions<V> & SelectStateRenderProps<V>>;
export type AccordionMultipleUncontrolledProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, AccordionMultipleUncontrolledBaseProps<V>>;
export type AccordionProps<V, T extends ValidConstructor = 'div'> = AccordionSingleControlledProps<V, T> | AccordionSingleUncontrolledProps<V, T> | AccordionMultipleControlledProps<V, T> | AccordionMultipleUncontrolledProps<V, T>;
/**
 * A set of vertically stacked sections, each of which can be expanded to
 * reveal its content. Wraps a select state, so `defaultValue`/`value` hold the
 * id of the open section, or an array of ids when `multiple` is set.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/accordion.md}
 */
export declare function Accordion<V, T extends ValidConstructor = 'div'>(props: AccordionProps<V, T>): JSX.Element;
//#endregion
//#region src/states/create-select-option-state.d.ts
interface SelectOptionStateOptions<T> {
  value: T;
  disabled?: boolean;
}
interface SelectOptionStateProperties {
  isSelected: () => boolean;
  select: () => void;
  isActive: () => boolean;
  focus: () => void;
  blur: () => void;
  disabled: () => boolean;
}
/**
 * Creates one option's view of the nearest select state, so the option can ask
 * whether it is selected or active without knowing about the others.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#select-option-state}
 */
export declare function createSelectOptionState<T>(options: SelectOptionStateOptions<T>): SelectOptionStateProperties;
interface SelectOptionStateRenderProps {
  children?: JSX.Element | ((state: SelectOptionStateProperties) => JSX.Element);
}
/**
 * Reads the nearest select option state from context. Throws when there is
 * none.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#select-option-state}
 */
export declare function useSelectOptionState(): SelectOptionStateProperties;
/**
 * Passes the nearest select option state to a render prop. A function child is
 * treated as a render prop only when it declares exactly one parameter.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#select-option-state}
 */
export declare function SelectOptionStateChild(props: SelectOptionStateRenderProps): JSX.Element;
//#endregion
//#region src/components/button/index.d.ts
interface ButtonBaseProps {
  disabled?: boolean;
}
export type ButtonProps<T extends ValidConstructor = 'button'> = HeadlessPropsWithRef<T, ButtonBaseProps>;
/**
 * Button behaviour on any element. On a real `<button>` this only adds the
 * disabled handling; on anything else it also supplies `role="button"`,
 * `tabindex`, and <kbd>Enter</kbd>/<kbd>Space</kbd> activation.
 *
 * Renders a `<button>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/button.md}
 */
export declare function Button<T extends ValidConstructor = 'button'>(props: ButtonProps<T>): JSX.Element;
//#endregion
//#region src/components/accordion/AccordionButton.d.ts
export type AccordionButtonProps<T extends ValidConstructor = 'button'> = HeadlessPropsWithRef<T, OmitAndMerge<SelectOptionStateRenderProps, ButtonProps<T>>>;
/**
 * The control that expands and collapses its `AccordionItem`. Carries `aria-
 * expanded` and `aria-controls`, and takes part in the accordion's arrow-key
 * navigation.
 *
 * Renders a `<button>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/accordion.md}
 */
export declare function AccordionButton<T extends ValidConstructor = 'button'>(props: AccordionButtonProps<T>): JSX.Element;
//#endregion
//#region src/components/accordion/AccordionHeader.d.ts
export type AccordionHeaderProps<T extends ValidConstructor = 'h3'> = HeadlessProps<T, SelectOptionStateRenderProps>;
/**
 * The heading that wraps an `AccordionButton`. Needed so screen readers can
 * list the sections by their headings.
 *
 * Renders an `<h3>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/accordion.md}
 */
export declare function AccordionHeader<T extends ValidConstructor = 'h3'>(props: AccordionHeaderProps<T>): JSX.Element;
//#endregion
//#region src/components/accordion/AccordionItem.d.ts
export type AccordionItemprops<V> = Prettify<SelectOptionStateOptions<V> & SelectOptionStateRenderProps>;
export type AccordionItemProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, AccordionItemprops<V>>;
/**
 * One section of an `Accordion`. The required `value` prop is the id this
 * section is selected by.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/accordion.md}
 */
export declare function AccordionItem<V, T extends ValidConstructor = 'div'>(props: AccordionItemProps<V, T>): JSX.Element;
//#endregion
//#region src/utils/create-unmountable.d.ts
interface UnmountableProps {
  unmount?: boolean | 'offscreen';
}
//#endregion
//#region src/components/accordion/AccordionPanel.d.ts
export type AccordionPanelBaseProps = Prettify<SelectOptionStateRenderProps & UnmountableProps>;
export type AccordionPanelProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, AccordionPanelBaseProps>;
/**
 * The content revealed when its `AccordionItem` is expanded. Unmounts while
 * collapsed unless `unmount={false}` is set.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/accordion.md}
 */
export declare function AccordionPanel<T extends ValidConstructor = 'div'>(props: AccordionPanelProps<T>): JSX.Element;
//#endregion
//#region src/components/alert/index.d.ts
export type AlertProps<T extends ValidConstructor = 'div'> = HeadlessProps<T>;
/**
 * A live region for a message that needs attention as soon as it appears, such
 * as a form error. Assistive technology announces its content without moving
 * focus.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/alert.md}
 */
export declare function Alert<T extends ValidConstructor = 'div'>(props: AlertProps<T>): JSX.Element;
//#endregion
//#region src/states/create-disclosure-state.d.ts
interface DisclosureStateControlledOptions {
  isOpen: boolean;
  disabled?: boolean;
  onChange?: (state: boolean) => void;
  onClose?: () => void;
  onOpen?: () => void;
}
interface DisclosureStateUncontrolledOptions {
  defaultOpen: boolean;
  disabled?: boolean;
  onChange?: (state: boolean) => void;
  onClose?: () => void;
  onOpen?: () => void;
}
type DisclosureStateOptions = DisclosureStateControlledOptions | DisclosureStateUncontrolledOptions;
interface DisclosureStateProperties {
  isOpen: () => boolean;
  setState: (newState: boolean) => void;
  disabled: () => boolean;
  close: () => void;
  open: () => void;
  toggle: () => void;
}
/**
 * Creates an open/closed state. Backs `Disclosure`, `Dialog`, `AlertDialog`,
 * `Popover`, `ContextMenu`, `CommandBar` and the popups of `Listbox` and
 * `Combobox`.
 *
 * Pass `defaultOpen` for uncontrolled state or `isOpen` for controlled; the
 * two are mutually exclusive.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#disclosure-state}
 */
export declare function createDisclosureState(options: DisclosureStateOptions): DisclosureStateProperties;
interface DisclosureStateRenderProps {
  children?: JSX.Element | ((state: DisclosureStateProperties) => JSX.Element);
}
/**
 * Reads the nearest disclosure state from context. Throws when there is none.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#disclosure-state}
 */
export declare function useDisclosureState(): DisclosureStateProperties;
/**
 * Passes the nearest disclosure state to a render prop. A function child is
 * treated as a render prop only when it declares exactly one parameter.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#disclosure-state}
 */
export declare function DisclosureStateChild(props: DisclosureStateRenderProps): JSX.Element;
//#endregion
//#region src/components/alert-dialog/AlertDialog.d.ts
export type AlertDialogControlledBaseProps = Prettify<DisclosureStateControlledOptions & DisclosureStateRenderProps & UnmountableProps>;
export type AlertDialogControlledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, AlertDialogControlledBaseProps>;
export type AlertDialogUncontrolledBaseProps = Prettify<DisclosureStateUncontrolledOptions & DisclosureStateRenderProps & UnmountableProps>;
export type AlertDialogUncontrolledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, AlertDialogUncontrolledBaseProps>;
export type AlertDialogProps<T extends ValidConstructor = 'div'> = AlertDialogControlledProps<T> | AlertDialogUncontrolledProps<T>;
/**
 * A modal that interrupts the user to confirm an action. Same behaviour as
 * `Dialog`, but with `role="alertdialog"`, so it is announced immediately. Use
 * it only for messages that require a response.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/alert-dialog.md}
 */
export declare function AlertDialog<T extends ValidConstructor = 'div'>(props: AlertDialogProps<T>): JSX.Element;
//#endregion
//#region src/components/alert-dialog/AlertDialogDescription.d.ts
export type AlertDialogDescriptionProps<T extends ValidConstructor = 'p'> = HeadlessProps<T, DisclosureStateRenderProps>;
/**
 * The accessible description of an `AlertDialog`, wired up through `aria-
 * describedby`.
 *
 * Renders a `<p>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/alert-dialog.md}
 */
export declare function AlertDialogDescription<T extends ValidConstructor = 'p'>(props: AlertDialogDescriptionProps<T>): JSX.Element;
//#endregion
//#region src/components/alert-dialog/AlertDialogOverlay.d.ts
export type AlertDialogOverlayProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The backdrop behind an `AlertDialog`. Clicking it closes the dialog, so give
 * it a size — it has no styles of its own and renders 0x0 without them.
 *
 * A full-screen overlay is positioned, so it paints above an unpositioned
 * sibling: give `AlertDialogPanel` a `position` or a `z-index` of its own, or
 * the overlay covers it and swallows the clicks meant for it.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/alert-dialog.md}
 */
export declare function AlertDialogOverlay<T extends ValidConstructor = 'div'>(props: AlertDialogOverlayProps<T>): JSX.Element;
//#endregion
//#region src/components/alert-dialog/AlertDialogPanel.d.ts
export type AlertDialogPanelProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The content of an `AlertDialog`. Traps `Tab` while the dialog is open and
 * restores focus to the trigger on close.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/alert-dialog.md}
 */
export declare function AlertDialogPanel<T extends ValidConstructor = 'div'>(props: AlertDialogPanelProps<T>): JSX.Element;
//#endregion
//#region src/components/alert-dialog/AlertDialogTitle.d.ts
export type AlertDialogTitleProps<T extends ValidConstructor = 'h2'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The accessible name of an `AlertDialog`, wired up through `aria-labelledby`.
 *
 * Renders an `<h2>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/alert-dialog.md}
 */
export declare function AlertDialogTitle<T extends ValidConstructor = 'h2'>(props: AlertDialogTitleProps<T>): JSX.Element;
//#endregion
//#region src/states/create-check-state.d.ts
interface CheckStateControlledOptions {
  checked: boolean | undefined;
  disabled?: boolean;
  onChange?: (state?: boolean) => void;
}
interface CheckStateUncontrolledOptions {
  defaultChecked: boolean | undefined;
  disabled?: boolean;
  onChange?: (state?: boolean) => void;
}
type CheckStateOptions = CheckStateControlledOptions | CheckStateUncontrolledOptions;
interface CheckStateProperties {
  checked: () => boolean | undefined;
  setState: (newState?: boolean) => void;
  disabled: () => boolean;
  check: () => void;
  uncheck: () => void;
  reset: () => void;
  toggle: () => void;
}
/**
 * Creates a tri-state checkbox value: `true`, `false`, or `undefined` for
 * indeterminate. Backs `Checkbox`.
 *
 * Pass `defaultChecked` for uncontrolled state or `checked` for controlled.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#check-state}
 */
export declare function createCheckState(options: CheckStateOptions): CheckStateProperties;
interface CheckStateRenderProps {
  children?: JSX.Element | ((state: CheckStateProperties) => JSX.Element);
}
/**
 * Reads the nearest check state from context. Throws when there is none.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#check-state}
 */
export declare function useCheckState(): CheckStateProperties;
/**
 * Passes the nearest check state to a render prop. A function child is treated
 * as a render prop only when it declares exactly one parameter.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#check-state}
 */
export declare function CheckStateChild(props: CheckStateRenderProps): JSX.Element;
//#endregion
//#region src/components/checkbox/Checkbox.d.ts
export type CheckboxControlledBaseProps = Prettify<CheckStateControlledOptions & CheckStateRenderProps>;
export type CheckboxControlledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, CheckboxControlledBaseProps>;
export type CheckboxUncontrolledBaseProps = Prettify<CheckStateUncontrolledOptions & CheckStateRenderProps>;
export type CheckboxUncontrolledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, CheckboxUncontrolledBaseProps>;
export type CheckboxProps<T extends ValidConstructor = 'div'> = CheckboxControlledProps<T> | CheckboxUncontrolledProps<T>;
/**
 * A checkbox that can be checked, unchecked, or indeterminate. It is a wrapper
 * only: the tickable control is `CheckboxIndicator`, and the state lives in
 * `defaultChecked`/`checked`, where `undefined` means indeterminate.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/checkbox.md}
 */
export declare function Checkbox<T extends ValidConstructor = 'div'>(props: CheckboxProps<T>): JSX.Element;
//#endregion
//#region src/components/checkbox/CheckboxDescription.d.ts
export type CheckboxDescriptionProps<T extends ValidConstructor = 'p'> = HeadlessProps<T, CheckStateRenderProps>;
/**
 * The accessible description of a `Checkbox`, wired up through `aria-
 * describedby`.
 *
 * Renders a `<p>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/checkbox.md}
 */
export declare function CheckboxDescription<T extends ValidConstructor = 'p'>(props: CheckboxDescriptionProps<T>): JSX.Element;
//#endregion
//#region src/components/checkbox/CheckboxIndicator.d.ts
export type CheckboxIndicatorProps<T extends ValidConstructor = 'button'> = HeadlessPropsWithRef<T, CheckStateRenderProps>;
/**
 * The control the user actually clicks. Carries `role="checkbox"` and `aria-
 * checked`, which is `"mixed"` while the state is indeterminate.
 *
 * Renders a `<button>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/checkbox.md}
 */
export declare function CheckboxIndicator<T extends ValidConstructor = 'button'>(props: CheckboxIndicatorProps<T>): JSX.Element;
//#endregion
//#region src/components/checkbox/CheckboxLabel.d.ts
export type CheckboxLabelProps<T extends ValidConstructor = 'label'> = HeadlessProps<T, CheckStateRenderProps>;
/**
 * The accessible name of a `Checkbox`, wired up through `aria-labelledby`.
 *
 * Renders a `<label>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/checkbox.md}
 */
export declare function CheckboxLabel<T extends ValidConstructor = 'label'>(props: CheckboxLabelProps<T>): JSX.Element;
//#endregion
//#region src/components/color-scheme/index.d.ts
export type NativeColorScheme = 'light' | 'dark';
export type ColorScheme = NativeColorScheme | 'system';
export interface ColorSchemeProviderControlledProps {
  value: ColorScheme;
  onChange?: (scheme: ColorScheme) => void;
  children?: JSX.Element;
}
export interface ColorSchemeProviderUncontrolledProps {
  initialValue: ColorScheme;
  onChange?: (scheme: ColorScheme) => void;
  children?: JSX.Element;
}
export type ColorSchemeProviderProps = ColorSchemeProviderControlledProps | ColorSchemeProviderUncontrolledProps;
/**
 * Holds the chosen colour scheme, writes it to `localStorage` under `theme-
 * preference`, and reflects it as a `dark` class on the document element. Pass
 * `initialValue` to let it own the preference, or `value` and `onChange` to
 * store the preference somewhere else, such as a user account.
 *
 * Renders nothing of its own.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/color-scheme.md}
 */
export declare function ColorSchemeProvider(props: ColorSchemeProviderProps): JSX.Element;
/**
 * Reads and writes the chosen colour scheme: `'light'`, `'dark'` or
 * `'system'`. Returns a signal-like tuple. Throws when called outside a {@link
 * ColorSchemeProvider}.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/color-scheme.md}
 */
export declare function useColorScheme(): [() => ColorScheme, (newScheme: ColorScheme) => void];
/**
 * Reads what the operating system currently prefers, ignoring the user's
 * choice. Returns an accessor for `'light'` or `'dark'`.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/color-scheme.md}
 */
export declare function useNativeColorScheme(): () => NativeColorScheme;
/**
 * Reads the scheme that is actually in effect: the user's choice, or the
 * system preference when that choice is `'system'`. This is the one to style
 * from.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/color-scheme.md}
 */
export declare function usePreferredColorScheme(): () => NativeColorScheme;
//#endregion
//#region src/states/create-autocomplete-state.d.ts
interface AutocompleteStateProperties<T> {
  isSelected: (value: T) => boolean;
  select: (value: T) => void;
  hasSelected: () => boolean;
  isActive: (value: T) => boolean;
  hasActive: () => boolean;
  focus: (value: T) => void;
  blur: () => void;
  disabled: () => boolean;
  query: () => string;
  setQuery: (value: string) => void;
  matches: (value: T) => boolean;
  hasQuery: () => boolean;
}
interface SingleAutocompleteStateControlledOptions<T> {
  multiple?: false;
  toggleable?: boolean;
  /** `undefined` means nothing is selected, which is also what `toggleable` produces. */
  value: T | undefined;
  matchBy: (value: T, query: string) => boolean;
  onChange?: (value?: T) => void;
  disabled?: boolean;
  by?: (a: T, b: T) => boolean;
}
interface SingleAutocompleteStateUncontrolledOptions<T> {
  multiple?: false;
  toggleable?: boolean;
  /** `undefined` starts with nothing selected. */
  defaultValue: T | undefined;
  matchBy: (value: T, query: string) => boolean;
  onChange?: (value?: T) => void;
  disabled?: boolean;
  by?: (a: T, b: T) => boolean;
}
type SingleAutocompleteStateOptions<T> = SingleAutocompleteStateControlledOptions<T> | SingleAutocompleteStateUncontrolledOptions<T>;
/**
 * Creates a single-selection state with a debounced text query on top. Backs
 * `Combobox` and `Command`.
 *
 * The required `matchBy` decides which values survive the current query.
 * Writes to the query are debounced by 250ms, so `query()` lags typing.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#autocomplete-state}
 */
export declare function createSingleAutocompleteState<T>(options: SingleAutocompleteStateOptions<T>): AutocompleteStateProperties<T>;
interface MultipleAutocompleteStateControlledOptions<T> {
  multiple: true;
  toggleable?: boolean;
  value: T[];
  matchBy: (value: T, query: string) => boolean;
  onChange?: (value: T[]) => void;
  disabled?: boolean;
  by?: (a: T, b: T) => boolean;
}
interface MultipleAutocompleteStateUncontrolledOptions<T> {
  multiple: true;
  toggleable?: boolean;
  defaultValue: T[];
  matchBy: (value: T, query: string) => boolean;
  onChange?: (value: T[]) => void;
  disabled?: boolean;
  by?: (a: T, b: T) => boolean;
}
type MultipleAutocompleteStateOptions<T> = MultipleAutocompleteStateControlledOptions<T> | MultipleAutocompleteStateUncontrolledOptions<T>;
/**
 * Creates a multiple-selection state with a debounced text query on top.
 * Requires `multiple: true`.
 *
 * The required `matchBy` decides which values survive the current query.
 * Writes to the query are debounced by 250ms, so `query()` lags typing.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#autocomplete-state}
 */
export declare function createMultipleAutocompleteState<T>(options: MultipleAutocompleteStateOptions<T>): AutocompleteStateProperties<T>;
interface AutocompleteStateRenderProps<T> {
  children?: JSX.Element | ((state: AutocompleteStateProperties<T>) => JSX.Element);
}
/**
 * Reads the nearest autocomplete state from context. Throws when there is
 * none.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#autocomplete-state}
 */
export declare function useAutocompleteState<T>(): AutocompleteStateProperties<T>;
/**
 * Passes the nearest autocomplete state to a render prop. A function child is
 * treated as a render prop only when it declares exactly one parameter.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#autocomplete-state}
 */
export declare function AutocompleteStateChild<T>(props: AutocompleteStateRenderProps<T>): JSX.Element;
//#endregion
//#region src/components/combobox/Combobox.d.ts
export interface ComboboxBaseProps {
  onDisclosureChange?: (value: boolean) => void;
}
export interface ComboboxMultipleBaseProps<V> {
  onSelectChange?: (value: V[]) => void;
}
export interface ComboboxSingleBaseProps<V> {
  onSelectChange?: (value?: V) => void;
}
export type ComboboxSCSCDBaseProps<V> = Prettify<ComboboxBaseProps & ComboboxSingleBaseProps<V> & Omit<SingleAutocompleteStateControlledOptions<V>, 'onChange'> & Omit<DisclosureStateControlledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ComboboxSCSCDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ComboboxSCSCDBaseProps<V>>;
export type ComboboxSCSUDBaseProps<V> = Prettify<ComboboxBaseProps & ComboboxSingleBaseProps<V> & Omit<SingleAutocompleteStateControlledOptions<V>, 'onChange'> & Omit<DisclosureStateUncontrolledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ComboboxSCSUDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ComboboxSCSUDBaseProps<V>>;
export type ComboboxSUSCDBaseProps<V> = Prettify<ComboboxBaseProps & ComboboxSingleBaseProps<V> & Omit<SingleAutocompleteStateUncontrolledOptions<V>, 'onChange'> & Omit<DisclosureStateControlledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ComboboxSUSCDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ComboboxSUSCDBaseProps<V>>;
export type ComboboxSUSUDBaseProps<V> = Prettify<ComboboxBaseProps & ComboboxSingleBaseProps<V> & Omit<SingleAutocompleteStateUncontrolledOptions<V>, 'onChange'> & Omit<DisclosureStateUncontrolledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ComboboxSUSUDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ComboboxSUSUDBaseProps<V>>;
export type ComboboxSingleProps<V, T extends ValidConstructor = 'div'> = ComboboxSCSCDProps<V, T> | ComboboxSCSUDProps<V, T> | ComboboxSUSCDProps<V, T> | ComboboxSUSUDProps<V, T>;
export type ComboboxMCSCDBaseProps<V> = Prettify<ComboboxBaseProps & ComboboxMultipleBaseProps<V> & Omit<MultipleAutocompleteStateControlledOptions<V>, 'onChange'> & Omit<DisclosureStateControlledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ComboboxMCSCDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ComboboxMCSCDBaseProps<V>>;
export type ComboboxMCSUDBaseProps<V> = Prettify<ComboboxBaseProps & ComboboxMultipleBaseProps<V> & Omit<MultipleAutocompleteStateControlledOptions<V>, 'onChange'> & Omit<DisclosureStateUncontrolledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ComboboxMCSUDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ComboboxMCSUDBaseProps<V>>;
export type ComboboxMUSCDBaseProps<V> = Prettify<ComboboxBaseProps & ComboboxMultipleBaseProps<V> & Omit<MultipleAutocompleteStateUncontrolledOptions<V>, 'onChange'> & Omit<DisclosureStateControlledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ComboboxMUSCDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ComboboxMUSCDBaseProps<V>>;
export type ComboboxMUSUDBaseProps<V> = Prettify<ComboboxBaseProps & ComboboxMultipleBaseProps<V> & Omit<MultipleAutocompleteStateUncontrolledOptions<V>, 'onChange'> & Omit<DisclosureStateUncontrolledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ComboboxMUSUDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ComboboxMUSUDBaseProps<V>>;
export type ComboboxMultipleProps<V, T extends ValidConstructor = 'div'> = ComboboxMCSCDProps<V, T> | ComboboxMCSUDProps<V, T> | ComboboxMUSCDProps<V, T> | ComboboxMUSUDProps<V, T>;
export type ComboboxProps<V, T extends ValidConstructor = 'div'> = ComboboxMultipleProps<V, T> | ComboboxSingleProps<V, T>;
/**
 * A text input paired with a popup listbox that filters as you type. It owns
 * two states at once, so its callbacks are `onDisclosureChange` for the popup
 * and `onSelectChange` for the value. The required `by` and `matchBy` props
 * decide value equality and which options survive the current query.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/combobox.md}
 */
export declare function Combobox<V, T extends ValidConstructor = 'div'>(props: ComboboxProps<V, T>): JSX.Element;
//#endregion
//#region src/components/combobox/ComboboxInput.d.ts
export type ComboboxInputProps<T extends ValidConstructor = 'input'> = HeadlessPropsWithRef<T>;
/**
 * The text field of a `Combobox`. Typing sets the query, which is debounced by
 * 250ms, and the arrow keys move the active option through `aria-
 * activedescendant` while focus stays in the input.
 *
 * Renders an `<input>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/combobox.md}
 */
export declare function ComboboxInput<T extends ValidConstructor = 'input'>(props: ComboboxInputProps<T>): JSX.Element;
//#endregion
//#region src/components/combobox/ComboboxLabel.d.ts
export type ComboboxLabelProps<T extends ValidConstructor = 'label'> = HeadlessProps<T>;
/**
 * The accessible name of a `Combobox`, wired up through `aria-labelledby`.
 *
 * Renders a `<label>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/combobox.md}
 */
export declare function ComboboxLabel<T extends ValidConstructor = 'label'>(props: ComboboxLabelProps<T>): JSX.Element;
//#endregion
//#region src/states/create-autocomplete-option-state.d.ts
interface AutocompleteOptionStateOptions<T> {
  value: T;
  disabled?: boolean;
}
interface AutocompleteOptionStateProperties {
  isSelected: () => boolean;
  select: () => void;
  isActive: () => boolean;
  focus: () => void;
  blur: () => void;
  disabled: () => boolean;
  matches: () => boolean;
}
/**
 * Creates one option's view of the nearest autocomplete state, so the option
 * can ask whether it is selected, active, or a match for the current query.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#autocomplete-option-state}
 */
export declare function createAutocompleteOptionState<T>(options: AutocompleteOptionStateOptions<T>): AutocompleteOptionStateProperties;
interface AutocompleteOptionStateRenderProps {
  children?: JSX.Element | ((state: AutocompleteOptionStateProperties) => JSX.Element);
}
/**
 * Reads the nearest autocomplete option state from context. Throws when there
 * is none.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#autocomplete-option-state}
 */
export declare function useAutocompleteOptionState(): AutocompleteOptionStateProperties;
/**
 * Passes the nearest autocomplete option state to a render prop. A function
 * child is treated as a render prop only when it declares exactly one
 * parameter.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#autocomplete-option-state}
 */
export declare function AutocompleteOptionStateChild(props: AutocompleteOptionStateRenderProps): JSX.Element;
//#endregion
//#region src/components/combobox/ComboboxOption.d.ts
export type ComboboxOptionBaseProps<V> = Prettify<AutocompleteOptionStateOptions<V> & AutocompleteOptionStateRenderProps>;
export type ComboboxOptionProps<V, T extends ValidConstructor = 'li'> = HeadlessPropsWithRef<T, OmitAndMerge<ComboboxOptionBaseProps<V>, ButtonProps<T>>>;
/**
 * One option of a `Combobox`. Carries `tc-matches` while it matches the
 * current query, so options can be hidden with CSS instead of being unmounted.
 *
 * Renders an `<li>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/combobox.md}
 */
export declare function ComboboxOption<V, T extends ValidConstructor = 'li'>(props: ComboboxOptionProps<V, T>): JSX.Element;
//#endregion
//#region src/components/combobox/ComboboxOptions.d.ts
export type ComboboxOptionsBaseProps<V> = Prettify<UnmountableProps & AutocompleteStateRenderProps<V>>;
export type ComboboxOptionsProps<V, T extends ValidConstructor = 'ul'> = HeadlessPropsWithRef<T, ComboboxOptionsBaseProps<V>>;
/**
 * The popup list of a `Combobox`. Unmounts while closed unless
 * `unmount={false}` is set.
 *
 * Renders a `<ul>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/combobox.md}
 */
export declare function ComboboxOptions<V, T extends ValidConstructor = 'ul'>(props: ComboboxOptionsProps<V, T>): JSX.Element;
//#endregion
//#region src/components/command/Command.d.ts
export interface CommandBaseProps {
  horizontal?: boolean;
}
export type SingleCommandControlledBaseProps<V> = Prettify<CommandBaseProps & SingleAutocompleteStateControlledOptions<V> & AutocompleteStateRenderProps<V>>;
export type SingleCommandControlledProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, SingleCommandControlledBaseProps<V>>;
export type SingleCommandUncontrolledBaseProps<V> = Prettify<CommandBaseProps & SingleAutocompleteStateUncontrolledOptions<V> & AutocompleteStateRenderProps<V>>;
export type SingleCommandUncontrolledProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, SingleCommandUncontrolledBaseProps<V>>;
export type SingleCommandProps<V, T extends ValidConstructor = 'div'> = SingleCommandControlledProps<V, T> | SingleCommandUncontrolledProps<V, T>;
export type MultipleCommandControlledBaseProps<V> = Prettify<CommandBaseProps & MultipleAutocompleteStateControlledOptions<V> & AutocompleteStateRenderProps<V>>;
export type MultipleCommandControlledProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, MultipleCommandControlledBaseProps<V>>;
export type MultipleCommandUncontrolledBaseProps<V> = Prettify<CommandBaseProps & MultipleAutocompleteStateUncontrolledOptions<V> & AutocompleteStateRenderProps<V>>;
export type MultipleCommandUncontrolledProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, MultipleCommandUncontrolledBaseProps<V>>;
export type MultipleCommandProps<V, T extends ValidConstructor = 'div'> = MultipleCommandControlledProps<V, T> | MultipleCommandUncontrolledProps<V, T>;
export type CommandProps<V, T extends ValidConstructor = 'div'> = SingleCommandProps<V, T> | MultipleCommandProps<V, T>;
/**
 * An always-visible filtered listbox — the body of a command palette. Same
 * autocomplete state as `Combobox`, but with no popup of its own, so it can be
 * dropped inside a `CommandBar` or rendered inline.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command.md}
 */
export declare function Command<V, T extends ValidConstructor = 'div'>(props: CommandProps<V, T>): JSX.Element;
//#endregion
//#region src/components/command/CommandInput.d.ts
export type CommandInputProps<T extends ValidConstructor = 'input'> = HeadlessPropsWithRef<T>;
/**
 * The query field of a `Command`. Typing sets the query, which is debounced by
 * 250ms, and the arrow keys move the active option without moving focus out of
 * the input.
 *
 * Renders an `<input>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command.md}
 */
export declare function CommandInput<T extends ValidConstructor = 'input'>(props: CommandInputProps<T>): JSX.Element;
//#endregion
//#region src/components/command/CommandLabel.d.ts
export type CommandLabelProps<T extends ValidConstructor = 'label'> = HeadlessProps<T>;
/**
 * The accessible name of a `Command`, wired up through `aria-labelledby`.
 *
 * Renders a `<label>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command.md}
 */
export declare function CommandLabel<T extends ValidConstructor = 'label'>(props: CommandLabelProps<T>): JSX.Element;
//#endregion
//#region src/components/command/CommandOption.d.ts
export type CommandOptionBaseProps<V> = Prettify<AutocompleteOptionStateOptions<V> & AutocompleteOptionStateRenderProps>;
export type CommandOptionProps<V, T extends ValidConstructor = 'li'> = HeadlessPropsWithRef<T, OmitAndMerge<CommandOptionBaseProps<V>, ButtonProps<T>>>;
/**
 * One result in a `Command`. Carries `tc-matches` while it matches the current
 * query.
 *
 * Renders an `<li>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command.md}
 */
export declare function CommandOption<V, T extends ValidConstructor = 'li'>(props: CommandOptionProps<V, T>): JSX.Element;
//#endregion
//#region src/components/command/CommandOptions.d.ts
export type CommandOptionsProps<V, T extends ValidConstructor = 'ul'> = HeadlessPropsWithRef<T, AutocompleteStateRenderProps<V>>;
/**
 * The list of results in a `Command`.
 *
 * Renders a `<ul>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command.md}
 */
export declare function CommandOptions<V, T extends ValidConstructor = 'ul'>(props: CommandOptionsProps<V, T>): JSX.Element;
//#endregion
//#region src/components/command-bar/CommandBar.d.ts
export type CommandBarControlledBaseProps = Prettify<DisclosureStateControlledOptions & DisclosureStateRenderProps & UnmountableProps>;
export type CommandBarControlledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, CommandBarControlledBaseProps>;
export type CommandBarUncontrolledBaseProps = Prettify<DisclosureStateUncontrolledOptions & DisclosureStateRenderProps & UnmountableProps>;
export type CommandBarUncontrolledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, CommandBarUncontrolledBaseProps>;
export type CommandBarProps<T extends ValidConstructor = 'div'> = CommandBarControlledProps<T> | CommandBarUncontrolledProps<T>;
/**
 * A modal opened by a keyboard shortcut,
 * <kbd>Cmd</kbd>/<kbd>Ctrl</kbd>+<kbd>K</kbd> by default. It is a dialog, not
 * a palette on its own: put a `Command` inside it for the searchable part.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command-bar.md}
 */
export declare function CommandBar<T extends ValidConstructor = 'div'>(props: CommandBarProps<T>): JSX.Element;
//#endregion
//#region src/components/command-bar/CommandBarDescription.d.ts
export type CommandBarDescriptionProps<T extends ValidConstructor = 'p'> = HeadlessProps<T, DisclosureStateRenderProps>;
/**
 * The accessible description of a `CommandBar`, wired up through `aria-
 * describedby`.
 *
 * Renders a `<p>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command-bar.md}
 */
export declare function CommandBarDescription<T extends ValidConstructor = 'p'>(props: CommandBarDescriptionProps<T>): JSX.Element;
//#endregion
//#region src/components/command-bar/CommandBarOverlay.d.ts
export type CommandBarOverlayProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The backdrop behind a `CommandBar`. Clicking it closes the bar, so give it a
 * size — it has no styles of its own.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command-bar.md}
 */
export declare function CommandBarOverlay<T extends ValidConstructor = 'p'>(props: CommandBarOverlayProps<T>): JSX.Element;
//#endregion
//#region src/components/command-bar/CommandBarPanel.d.ts
export type CommandBarPanelProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The content of a `CommandBar`. Traps `Tab` while open and restores focus on
 * close.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command-bar.md}
 */
export declare function CommandBarPanel<T extends ValidConstructor = 'div'>(props: CommandBarPanelProps<T>): JSX.Element;
//#endregion
//#region src/components/command-bar/CommandBarTitle.d.ts
export type CommandBarTitleProps<T extends ValidConstructor = 'h2'> = HeadlessProps<T, DisclosureStateRenderProps>;
/**
 * The accessible name of a `CommandBar`, wired up through `aria-labelledby`.
 *
 * Renders an `<h2>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/command-bar.md}
 */
export declare function CommandBarTitle<T extends ValidConstructor = 'h2'>(props: CommandBarTitleProps<T>): JSX.Element;
//#endregion
//#region src/components/context-menu/ContextMenu.d.ts
export type ContextMenuControlledBaseProps = Prettify<DisclosureStateControlledOptions & DisclosureStateRenderProps>;
export type ContextMenuControlledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, ContextMenuControlledBaseProps>;
export type ContextMenuUncontrolledBaseProps = Prettify<DisclosureStateUncontrolledOptions & DisclosureStateRenderProps>;
export type ContextMenuUncontrolledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, ContextMenuUncontrolledBaseProps>;
export type ContextMenuProps<T extends ValidConstructor = 'div'> = ContextMenuControlledProps<T> | ContextMenuUncontrolledProps<T>;
/**
 * A menu opened by right-click. It only manages open state and the trap; the
 * menu's own arrow-key navigation comes from putting a `Menu` inside the
 * panel.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/context-menu.md}
 */
export declare function ContextMenu<T extends ValidConstructor = 'div'>(props: ContextMenuProps<T>): JSX.Element;
//#endregion
//#region src/components/context-menu/ContextMenuBoundary.d.ts
export type ContextMenuBoundaryProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The region that listens for right-clicks. Opening the menu suppresses the
 * browser's own context menu inside this element only.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/context-menu.md}
 */
export declare function ContextMenuBoundary<T extends ValidConstructor = 'div'>(props: ContextMenuBoundaryProps<T>): JSX.Element;
//#endregion
//#region src/components/context-menu/ContextMenuOverlay.d.ts
export type ContextMenuOverlayProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The backdrop behind a `ContextMenu`. Clicking it closes the menu, so give it
 * a size — it has no styles of its own. It is never unmounted, unlike the
 * panel, so hide it with CSS or a `<Show>` while closed, or it will swallow
 * clicks on the page.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/context-menu.md}
 */
export declare function ContextMenuOverlay<T extends ValidConstructor = 'div'>(props: ContextMenuOverlayProps<T>): JSX.Element;
//#endregion
//#region src/components/context-menu/ContextMenuPanel.d.ts
export type ContextMenuPanelBaseProps = Prettify<DisclosureStateRenderProps & UnmountableProps>;
export type ContextMenuPanelProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, ContextMenuPanelBaseProps>;
/**
 * The floating panel of a `ContextMenu`. Traps `Tab` while open and closes on
 * <kbd>Escape</kbd>. Position it yourself — the library sets no coordinates.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/context-menu.md}
 */
export declare function ContextMenuPanel<T extends ValidConstructor = 'div'>(props: ContextMenuPanelProps<T>): JSX.Element;
//#endregion
//#region src/components/dialog/Dialog.d.ts
export type DialogControlledBaseProps = Prettify<DisclosureStateControlledOptions & DisclosureStateRenderProps & UnmountableProps>;
export type DialogControlledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, DialogControlledBaseProps>;
export type DialogUncontrolledBaseProps = Prettify<DisclosureStateUncontrolledOptions & DisclosureStateRenderProps & UnmountableProps>;
export type DialogUncontrolledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, DialogUncontrolledBaseProps>;
export type DialogProps<T extends ValidConstructor = 'div'> = DialogControlledProps<T> | DialogUncontrolledProps<T>;
/**
 * A modal dialog. While it is open the panel traps `Tab`, <kbd>Escape</kbd>
 * closes it, and focus returns to whatever opened it. Rendering it into a
 * portal is up to you.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/dialog.md}
 */
export declare function Dialog<T extends ValidConstructor = 'div'>(props: DialogProps<T>): JSX.Element;
//#endregion
//#region src/components/dialog/DialogDescription.d.ts
export type DialogDescriptionProps<T extends ValidConstructor = 'p'> = HeadlessProps<T, DisclosureStateRenderProps>;
/**
 * The accessible description of a `Dialog`, wired up through `aria-
 * describedby`.
 *
 * Renders a `<p>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/dialog.md}
 */
export declare function DialogDescription<T extends ValidConstructor = 'p'>(props: DialogDescriptionProps<T>): JSX.Element;
//#endregion
//#region src/components/dialog/DialogOverlay.d.ts
export type DialogOverlayProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The backdrop behind a `Dialog`. Clicking it closes the dialog, so give it a
 * size — it has no styles of its own and renders 0x0 without them. It needs no
 * `<Show>` guard: `Dialog` unmounts its whole subtree while closed.
 *
 * A full-screen overlay is positioned, so it paints above an unpositioned
 * sibling: give `DialogPanel` a `position` or a `z-index` of its own, or the
 * overlay covers it and swallows the clicks meant for it.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/dialog.md}
 */
export declare function DialogOverlay<T extends ValidConstructor = 'div'>(props: DialogOverlayProps<T>): JSX.Element;
//#endregion
//#region src/components/dialog/DialogPanel.d.ts
export type DialogPanelProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The content of a `Dialog`, and the element that traps focus.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/dialog.md}
 */
export declare function DialogPanel<T extends ValidConstructor = 'div'>(props: DialogPanelProps<T>): JSX.Element;
//#endregion
//#region src/components/dialog/DialogTitle.d.ts
export type DialogTitleProps<T extends ValidConstructor = 'h2'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The accessible name of a `Dialog`, wired up through `aria-labelledby`.
 *
 * Renders an `<h2>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/dialog.md}
 */
export declare function DialogTitle<T extends ValidConstructor = 'h2'>(props: DialogTitleProps<T>): JSX.Element;
//#endregion
//#region src/components/disclosure/Disclosure.d.ts
export type DisclosureControlledBaseProps = Prettify<DisclosureStateControlledOptions & DisclosureStateRenderProps>;
export type DisclosureControlledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, DisclosureControlledBaseProps>;
export type DisclosureUncontrolledBaseProps = Prettify<DisclosureStateUncontrolledOptions & DisclosureStateRenderProps>;
export type DisclosureUncontrolledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, DisclosureUncontrolledBaseProps>;
export type DisclosureProps<T extends ValidConstructor = 'div'> = DisclosureControlledProps<T> | DisclosureUncontrolledProps<T>;
/**
 * A button that shows and hides a section. The simplest stateful component in
 * the library, and the base the dialog-like components are built on.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/disclosure.md}
 */
export declare function Disclosure<T extends ValidConstructor = 'div'>(props: DisclosureProps<T>): JSX.Element;
//#endregion
//#region src/components/disclosure/DisclosureButton.d.ts
export type DisclosureButtonProps<T extends ValidConstructor = 'button'> = HeadlessPropsWithRef<T, OmitAndMerge<DisclosureStateRenderProps, ButtonProps<T>>>;
/**
 * The control that toggles a `Disclosure`. Carries `aria-expanded`, and `aria-
 * controls` while the panel is mounted.
 *
 * Renders a `<button>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/disclosure.md}
 */
export declare function DisclosureButton<T extends ValidConstructor = 'button'>(props: DisclosureButtonProps<T>): JSX.Element;
//#endregion
//#region src/components/disclosure/DisclosurePanel.d.ts
export type DisclosurePanelBaseProps = Prettify<DisclosureStateRenderProps & UnmountableProps>;
export type DisclosurePanelProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, DisclosurePanelBaseProps>;
/**
 * The section a `Disclosure` shows and hides. Unmounts while closed unless
 * `unmount={false}` is set.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/disclosure.md}
 */
export declare function DisclosurePanel<T extends ValidConstructor = 'div'>(props: DisclosurePanelProps<T>): JSX.Element;
//#endregion
//#region src/components/feed/Feed.d.ts
export interface FeedBaseProps {
  size: number;
  busy?: boolean;
}
export type FeedProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, FeedBaseProps>;
/**
 * A stream of articles with the feed keyboard pattern: <kbd>Page Down</kbd>
 * and <kbd>Page Up</kbd> move between articles,
 * <kbd>Ctrl</kbd>+<kbd>Home</kbd> and <kbd>Ctrl</kbd>+<kbd>End</kbd> jump to
 * the ends. Set `size` to the total number of articles, or `-1` when it is
 * unknown, and `busy` while more are loading.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/feed.md}
 */
export declare function Feed<T extends ValidConstructor = 'div'>(props: FeedProps<T>): JSX.Element;
//#endregion
//#region src/components/feed/FeedArticle.d.ts
export type FeedArticleProps<T extends ValidConstructor = 'article'> = HeadlessPropsWithRef<T, {
  index: number;
}>;
/**
 * One entry in a `Feed`. The required `index` prop is its zero-based position,
 * which becomes `aria-posinset`.
 *
 * Renders an `<article>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/feed.md}
 */
export declare function FeedArticle<T extends ValidConstructor = 'article'>(props: FeedArticleProps<T>): JSX.Element;
//#endregion
//#region src/components/feed/FeedArticleDescription.d.ts
export type FeedArticleDescriptionProps<T extends ValidConstructor = 'p'> = HeadlessProps<T>;
/**
 * The accessible description of a `FeedArticle`, wired up through `aria-
 * describedby`.
 *
 * Renders a `<p>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/feed.md}
 */
export declare function FeedArticleDescription<T extends ValidConstructor = 'p'>(props: FeedArticleDescriptionProps<T>): JSX.Element;
//#endregion
//#region src/components/feed/FeedArticleLabel.d.ts
export type FeedArticleLabelProps<T extends ValidConstructor = 'span'> = HeadlessProps<T>;
/**
 * The accessible name of a `FeedArticle`, wired up through `aria-labelledby`.
 *
 * Renders a `<span>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/feed.md}
 */
export declare function FeedArticleLabel<T extends ValidConstructor = 'span'>(props: FeedArticleLabelProps<T>): JSX.Element;
//#endregion
//#region src/components/feed/FeedContent.d.ts
export type FeedContentProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T>;
/**
 * The scrolling region that holds the articles of a `Feed`. Everything outside
 * it, such as a load-more button, stays out of the feed's navigation.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/feed.md}
 */
export declare function FeedContent<T extends ValidConstructor = 'div'>(props: FeedContentProps<T>): JSX.Element;
//#endregion
//#region src/components/feed/FeedLabel.d.ts
export type FeedLabelProps<T extends ValidConstructor = 'span'> = HeadlessProps<T>;
/**
 * The accessible name of a `Feed`, wired up through `aria-labelledby`.
 *
 * Renders a `<span>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/feed.md}
 */
export declare function FeedLabel<T extends ValidConstructor = 'span'>(props: FeedLabelProps<T>): JSX.Element;
//#endregion
//#region src/components/listbox/Listbox.d.ts
export interface ListboxBaseProps {
  horizontal?: boolean;
  onDisclosureChange?: (value: boolean) => void;
}
export interface ListboxMultipleBaseProps<V> {
  onSelectChange?: (value: V[]) => void;
}
export interface ListboxSingleBaseProps<V> {
  onSelectChange?: (value?: V) => void;
}
export type ListboxSCSCDBaseProps<V> = Prettify<ListboxBaseProps & ListboxSingleBaseProps<V> & Omit<SingleSelectStateControlledOptions<V>, 'onChange'> & Omit<DisclosureStateControlledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ListboxSCSCDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ListboxSCSCDBaseProps<V>>;
export type ListboxSCSUDBaseProps<V> = Prettify<ListboxBaseProps & ListboxSingleBaseProps<V> & Omit<SingleSelectStateControlledOptions<V>, 'onChange'> & Omit<DisclosureStateUncontrolledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ListboxSCSUDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ListboxSCSUDBaseProps<V>>;
export type ListboxSUSCDBaseProps<V> = Prettify<ListboxBaseProps & ListboxSingleBaseProps<V> & Omit<SingleSelectStateUncontrolledOptions<V>, 'onChange'> & Omit<DisclosureStateControlledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ListboxSUSCDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ListboxSUSCDBaseProps<V>>;
export type ListboxSUSUDBaseProps<V> = Prettify<ListboxBaseProps & ListboxSingleBaseProps<V> & Omit<SingleSelectStateUncontrolledOptions<V>, 'onChange'> & Omit<DisclosureStateUncontrolledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ListboxSUSUDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ListboxSUSUDBaseProps<V>>;
export type ListboxSingleProps<V, T extends ValidConstructor = 'div'> = ListboxSCSCDProps<V, T> | ListboxSCSUDProps<V, T> | ListboxSUSCDProps<V, T> | ListboxSUSUDProps<V, T>;
export type ListboxMCSCDBaseProps<V> = Prettify<ListboxBaseProps & ListboxMultipleBaseProps<V> & Omit<MultipleSelectStateControlledOptions<V>, 'onChange'> & Omit<DisclosureStateControlledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ListboxMCSCDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ListboxMCSCDBaseProps<V>>;
export type ListboxMCSUDBaseProps<V> = Prettify<ListboxBaseProps & ListboxMultipleBaseProps<V> & Omit<MultipleSelectStateControlledOptions<V>, 'onChange'> & Omit<DisclosureStateUncontrolledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ListboxMCSUDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ListboxMCSUDBaseProps<V>>;
export type ListboxMUSCDBaseProps<V> = Prettify<ListboxBaseProps & ListboxMultipleBaseProps<V> & Omit<MultipleSelectStateUncontrolledOptions<V>, 'onChange'> & Omit<DisclosureStateControlledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ListboxMUSCDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ListboxMUSCDBaseProps<V>>;
export type ListboxMUSUDBaseProps<V> = Prettify<ListboxBaseProps & ListboxMultipleBaseProps<V> & Omit<MultipleSelectStateUncontrolledOptions<V>, 'onChange'> & Omit<DisclosureStateUncontrolledOptions, 'onChange'> & {
  children?: JSX.Element;
}>;
export type ListboxMUSUDProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, ListboxMUSUDBaseProps<V>>;
export type ListboxMultipleProps<V, T extends ValidConstructor = 'div'> = ListboxMCSCDProps<V, T> | ListboxMCSUDProps<V, T> | ListboxMUSCDProps<V, T> | ListboxMUSUDProps<V, T>;
export type ListboxProps<V, T extends ValidConstructor = 'div'> = ListboxMultipleProps<V, T> | ListboxSingleProps<V, T>;
/**
 * A dropdown select: a button showing the current value, plus a popup list of
 * options. It owns two states at once, so its callbacks are
 * `onDisclosureChange` for the popup and `onSelectChange` for the value.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/listbox.md}
 */
export declare function Listbox<V, T extends ValidConstructor = 'div'>(props: ListboxProps<V, T>): JSX.Element;
//#endregion
//#region src/components/listbox/ListboxButton.d.ts
export type ListboxButtonProps<T extends ValidConstructor = 'button'> = HeadlessPropsWithRef<T, OmitAndMerge<DisclosureStateRenderProps, ButtonProps<T>>>;
/**
 * The trigger of a `Listbox`. Carries `aria-expanded` and `aria-haspopup`, and
 * opens the popup with the arrow keys as well as by click.
 *
 * Renders a `<button>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/listbox.md}
 */
export declare function ListboxButton<T extends ValidConstructor = 'button'>(props: ListboxButtonProps<T>): JSX.Element;
//#endregion
//#region src/components/listbox/ListboxLabel.d.ts
export type ListboxLabelProps<T extends ValidConstructor = 'label'> = HeadlessProps<T, DisclosureStateRenderProps>;
/**
 * The accessible name of a `Listbox`, wired up through `aria-labelledby`.
 *
 * Renders a `<label>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/listbox.md}
 */
export declare function ListboxLabel<T extends ValidConstructor = 'label'>(props: ListboxLabelProps<T>): JSX.Element;
//#endregion
//#region src/components/listbox/ListboxOption.d.ts
export type ListboxOptionBaseProps<V> = Prettify<SelectOptionStateOptions<V> & SelectOptionStateRenderProps>;
export type ListboxOptionProps<V, T extends ValidConstructor = 'li'> = HeadlessPropsWithRef<T, OmitAndMerge<ListboxOptionBaseProps<V>, ButtonProps<T>>>;
/**
 * One option of a `Listbox`. The required `value` prop is what selecting it
 * produces.
 *
 * Renders an `<li>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/listbox.md}
 */
export declare function ListboxOption<V, T extends ValidConstructor = 'li'>(props: ListboxOptionProps<V, T>): JSX.Element;
//#endregion
//#region src/components/listbox/ListboxOptions.d.ts
export type ListboxOptionsBaseProps<V> = Prettify<UnmountableProps & SelectStateRenderProps<V>>;
export type ListboxOptionsProps<V, T extends ValidConstructor = 'ul'> = HeadlessPropsWithRef<T, ListboxOptionsBaseProps<V>>;
/**
 * The popup list of a `Listbox`. Unmounts while closed unless
 * `unmount={false}` is set.
 *
 * Renders a `<ul>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/listbox.md}
 */
export declare function ListboxOptions<V, T extends ValidConstructor = 'ul'>(props: ListboxOptionsProps<V, T>): JSX.Element;
//#endregion
//#region src/components/menu/Menu.d.ts
export type MenuProps<T extends ValidConstructor = 'ul'> = HeadlessPropsWithRef<T>;
/**
 * A menu of actions, navigated with the arrow keys and type-ahead. It has no
 * open state of its own; put it inside a `Popover` or `ContextMenu` for that.
 *
 * Per the ARIA menu pattern every item sits at `tabindex="-1"`, so the menu has
 * no tab stop and you must move focus to an item yourself when it appears.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/menu.md}
 */
export declare function Menu<T extends ValidConstructor = 'ul'>(props: MenuProps<T>): JSX.Element;
//#endregion
//#region src/components/menu/MenuChild.d.ts
export interface MenuProperties {
  disabled: () => boolean;
}
export type MenuChildRenderProp = (properties: MenuProperties) => JSX.Element;
export interface MenuChildProps {
  disabled?: boolean;
  children?: JSX.Element | MenuChildRenderProp;
}
/**
 * The render prop a `MenuItem` passes to its children, available as a
 * standalone component. It renders no element of its own, and reports its own
 * `disabled` prop rather than the surrounding item's.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/menu.md}
 */
export declare function MenuChild(props: MenuChildProps): JSX.Element;
//#endregion
//#region src/components/menu/MenuItem.d.ts
export type MenuItemProps<T extends ValidConstructor = 'li'> = HeadlessPropsWithRef<T, MenuChildProps>;
/**
 * One action in a `Menu`. The arrow keys and type-ahead skip disabled items.
 *
 * Renders an `<li>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/menu.md}
 */
export declare function MenuItem<T extends ValidConstructor = 'li'>(props: MenuItemProps<T>): JSX.Element;
//#endregion
//#region src/components/popover/Popover.d.ts
export type PopoverControlledBaseProps = Prettify<DisclosureStateRenderProps & DisclosureStateControlledOptions>;
export type PopoverControlledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, PopoverControlledBaseProps>;
export type PopoverUncontrolledBaseProps = Prettify<DisclosureStateRenderProps & DisclosureStateUncontrolledOptions>;
export type PopoverUncontrolledProps<T extends ValidConstructor = 'div'> = HeadlessProps<T, PopoverUncontrolledBaseProps>;
export type PopoverProps<T extends ValidConstructor = 'div'> = PopoverControlledProps<T> | PopoverUncontrolledProps<T>;
/**
 * A floating panel anchored to a button. Like a `Dialog` in that the panel can
 * trap `Tab`, but the page behind stays usable and the panel also closes when
 * focus leaves it.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/popover.md}
 */
export declare function Popover<T extends ValidConstructor = 'div'>(props: PopoverProps<T>): JSX.Element;
//#endregion
//#region src/components/popover/PopoverButton.d.ts
export type PopoverButtonProps<T extends ValidConstructor = 'button'> = HeadlessPropsWithRef<T, OmitAndMerge<DisclosureStateRenderProps, ButtonProps<T>>>;
/**
 * The trigger of a `Popover`. Carries `aria-expanded`, and `aria-controls`
 * while the panel is mounted.
 *
 * Renders a `<button>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/popover.md}
 */
export declare function PopoverButton<T extends ValidConstructor = 'button'>(props: PopoverButtonProps<T>): JSX.Element;
//#endregion
//#region src/components/popover/PopoverOverlay.d.ts
export type PopoverOverlayProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, DisclosureStateRenderProps>;
/**
 * The backdrop behind a `Popover`. Clicking it closes the popover, so give it
 * a size — it has no styles of its own. It is never unmounted, unlike the
 * panel, so hide it with CSS or a `<Show>` while closed, or it will swallow
 * clicks on the page.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/popover.md}
 */
export declare function PopoverOverlay<T extends ValidConstructor = 'div'>(props: PopoverOverlayProps<T>): JSX.Element;
//#endregion
//#region src/components/popover/PopoverPanel.d.ts
export type PopoverPanelBaseProps = Prettify<DisclosureStateRenderProps & UnmountableProps>;
export type PopoverPanelProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, PopoverPanelBaseProps>;
/**
 * The floating panel of a `Popover`. Position it yourself — the library sets
 * no coordinates.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/popover.md}
 */
export declare function PopoverPanel<T extends ValidConstructor = 'div'>(props: PopoverPanelProps<T>): JSX.Element;
//#endregion
//#region src/components/radio-group/RadioGroup.d.ts
export type RadioGroupControlledBaseProps<V> = Prettify<SingleSelectStateControlledOptions<V> & SelectStateRenderProps<V>>;
export type RadioGroupControlledProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, RadioGroupControlledBaseProps<V>>;
export type RadioGroupUncontrolledBaseProps<V> = Prettify<SingleSelectStateUncontrolledOptions<V> & SelectStateRenderProps<V>>;
export type RadioGroupUncontrolledProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, RadioGroupUncontrolledBaseProps<V>>;
export type RadioGroupProps<V, T extends ValidConstructor = 'div'> = RadioGroupControlledProps<V, T> | RadioGroupUncontrolledProps<V, T>;
/**
 * A single-choice group. The whole group is one tab stop; the arrow keys move
 * between options and select as they go.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/radio-group.md}
 */
export declare function RadioGroup<V, T extends ValidConstructor = 'div'>(props: RadioGroupProps<V, T>): JSX.Element;
//#endregion
//#region src/components/radio-group/RadioGroupDescription.d.ts
export type RadioGroupDescriptionProps<T extends ValidConstructor = 'div'> = HeadlessProps<T>;
/**
 * The accessible description of a `RadioGroup` or of one `RadioGroupOption`,
 * depending on which it is nested in. Wired up through `aria-describedby`.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/radio-group.md}
 */
export declare function RadioGroupDescription<T extends ValidConstructor = 'div'>(props: RadioGroupDescriptionProps<T>): JSX.Element;
//#endregion
//#region src/components/radio-group/RadioGroupLabel.d.ts
export type RadioGroupLabelProps<T extends ValidConstructor = 'label'> = HeadlessProps<T>;
/**
 * The accessible name of a `RadioGroup` or of one `RadioGroupOption`,
 * depending on which it is nested in. Wired up through `aria-labelledby`.
 *
 * Renders a `<label>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/radio-group.md}
 */
export declare function RadioGroupLabel<T extends ValidConstructor = 'label'>(props: RadioGroupLabelProps<T>): JSX.Element;
//#endregion
//#region src/components/radio-group/RadioGroupOption.d.ts
export type RadioGroupOptionBaseProps<V> = Prettify<SelectOptionStateOptions<V> & SelectOptionStateRenderProps>;
export type RadioGroupOptionProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, RadioGroupOptionBaseProps<V>>;
/**
 * One choice in a `RadioGroup`. The required `value` prop is what selecting it
 * produces.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/radio-group.md}
 */
export declare function RadioGroupOption<V, T extends ValidConstructor = 'div'>(props: RadioGroupOptionProps<V, T>): JSX.Element;
//#endregion
//#region src/components/select/Select.d.ts
export interface SelectBaseProps {
  horizontal?: boolean;
}
export type SingleSelectControlledBaseProps<V> = Prettify<SelectBaseProps & SingleSelectStateControlledOptions<V> & SelectStateRenderProps<V>>;
export type SingleSelectControlledProps<V, T extends ValidConstructor = 'ul'> = HeadlessPropsWithRef<T, SingleSelectControlledBaseProps<V>>;
export type SingleSelectUncontrolledBaseProps<V> = Prettify<SelectBaseProps & SingleSelectStateUncontrolledOptions<V> & SelectStateRenderProps<V>>;
export type SingleSelectUncontrolledProps<V, T extends ValidConstructor = 'ul'> = HeadlessPropsWithRef<T, SingleSelectUncontrolledBaseProps<V>>;
export type SingleSelectProps<V, T extends ValidConstructor = 'ul'> = SingleSelectControlledProps<V, T> | SingleSelectUncontrolledProps<V, T>;
export type MultipleSelectControlledBaseProps<V> = Prettify<SelectBaseProps & MultipleSelectStateControlledOptions<V> & SelectStateRenderProps<V>>;
export type MultipleSelectControlledProps<V, T extends ValidConstructor = 'ul'> = HeadlessPropsWithRef<T, MultipleSelectControlledBaseProps<V>>;
export type MultipleSelectUncontrolledBaseProps<V> = Prettify<SelectBaseProps & MultipleSelectStateUncontrolledOptions<V> & SelectStateRenderProps<V>>;
export type MultipleSelectUncontrolledProps<V, T extends ValidConstructor = 'ul'> = HeadlessPropsWithRef<T, MultipleSelectUncontrolledBaseProps<V>>;
export type MultipleSelectProps<V, T extends ValidConstructor = 'ul'> = MultipleSelectControlledProps<V, T> | MultipleSelectUncontrolledProps<V, T>;
export type SelectProps<V, T extends ValidConstructor = 'ul'> = SingleSelectProps<V, T> | MultipleSelectProps<V, T>;
/**
 * An always-visible listbox. The same selection behaviour as `Listbox` without
 * the popup, so it has one state instead of two and a single `onChange`.
 *
 * Renders a `<ul>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/select.md}
 */
export declare function Select<V, T extends ValidConstructor = 'ul'>(props: SelectProps<V, T>): JSX.Element;
//#endregion
//#region src/components/select/SelectOption.d.ts
export type SelectOptionBaseProps<V> = Prettify<SelectOptionStateOptions<V> & SelectOptionStateRenderProps>;
export type SelectOptionProps<V, T extends ValidConstructor = 'li'> = HeadlessPropsWithRef<T, OmitAndMerge<SelectOptionBaseProps<V>, ButtonProps<T>>>;
/**
 * One option of a `Select`. The required `value` prop is what selecting it
 * produces.
 *
 * Renders an `<li>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/select.md}
 */
export declare function SelectOption<V, T extends ValidConstructor = 'li'>(props: SelectOptionProps<V, T>): JSX.Element;
//#endregion
//#region src/components/tabs/Tab.d.ts
export type TabBaseProps<V> = Prettify<SelectOptionStateOptions<V> & SelectOptionStateRenderProps>;
export type TabProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, TabBaseProps<V>>;
/**
 * One tab in a `TabList`. The required `value` prop links it to the `TabPanel`
 * with the same value.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/tabs.md}
 */
export declare function Tab<V, T extends ValidConstructor = 'div'>(props: TabProps<V, T>): JSX.Element;
//#endregion
//#region src/components/tabs/TabGroup.d.ts
export interface TabGroupBaseProps {
  horizontal: boolean;
}
export type TabGroupControlledBaseProps<V> = Prettify<TabGroupBaseProps & SingleSelectStateControlledOptions<V> & SelectStateRenderProps<V>>;
export type TabGroupControlledProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, TabGroupControlledBaseProps<V>>;
export type TabGroupUncontrolledBaseProps<V> = Prettify<TabGroupBaseProps & SingleSelectStateUncontrolledOptions<V> & SelectStateRenderProps<V>>;
export type TabGroupUncontrolledProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, TabGroupUncontrolledBaseProps<V>>;
export type TabGroupProps<V, T extends ValidConstructor = 'div'> = TabGroupControlledProps<V, T> | TabGroupUncontrolledProps<V, T>;
/**
 * A tabbed interface. The `value` is the id of the selected tab, and the
 * arrow keys select as they move. The `horizontal` prop is required: it picks
 * which arrow keys navigate, and sets `aria-orientation`.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/tabs.md}
 */
export declare function TabGroup<V, T extends ValidConstructor = 'div'>(props: TabGroupProps<V, T>): JSX.Element;
//#endregion
//#region src/components/tabs/TabList.d.ts
export type TabListProps<V, T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, SelectStateRenderProps<V>>;
/**
 * The row of tabs in a `TabGroup`, and the element that owns their arrow-key
 * navigation.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/tabs.md}
 */
export declare function TabList<V, T extends ValidConstructor = 'div'>(props: TabListProps<V, T>): JSX.Element;
//#endregion
//#region src/components/tabs/TabPanel.d.ts
export interface TabPanelBaseProps<V> extends Exclude<SelectOptionStateOptions<V>, 'disabled'> {
  unmount?: boolean;
}
export type TabPanelProps<V, T extends ValidConstructor = 'div'> = HeadlessProps<T, TabPanelBaseProps<V>>;
/**
 * The content shown for the `Tab` with the same `value`. Unmounts while its
 * tab is unselected unless `unmount={false}` is set.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/tabs.md}
 */
export declare function TabPanel<V, T extends ValidConstructor = 'div'>(props: TabPanelProps<V, T>): JSX.Element;
//#endregion
//#region src/components/toast/index.d.ts
export type ToastProps<T extends ValidConstructor = 'div'> = HeadlessProps<T>;
/**
 * One notification inside a {@link Toaster}. Carries `role="status"`, so it is
 * announced without stealing focus.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/toast.md}
 */
export declare function Toast<T extends ValidConstructor = 'div'>(props: ToastProps<T>): JSX.Element;
export type ToasterProps<T extends ValidConstructor = 'div'> = HeadlessProps<T>;
/**
 * The region that holds the toasts. It does not read the queue for you:
 * subscribe with {@link useToaster} and map over the result yourself.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/toast.md}
 */
export declare function Toaster<T extends ValidConstructor = 'div'>(props: ToasterProps<T>): JSX.Element;
export interface ToastData<T> {
  id: string;
  data: T;
}
export type ToasterListener<T> = (queue: ToastData<T>[]) => void;
/**
 * The queue behind a {@link Toaster}. Create one at module scope and share it,
 * so any code can push a toast with `create`, drop one with `remove`, or empty
 * the queue with `clear`.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/toast.md}
 */
export declare class ToasterStore<T> {
  private static toasterID;
  private readonly id;
  private queue;
  private readonly listeners;
  private toastID;
  constructor();
  subscribe(callback: ToasterListener<T>): () => void;
  private notify;
  create(data: T): string;
  remove(id: string): void;
  clear(): void;
  getQueue(): ToastData<T>[];
}
/**
 * Subscribes to a {@link ToasterStore} and returns its queue as a signal. The
 * store is passed in rather than read from context, so the same queue can be
 * reached from anywhere in the app, including outside the component tree.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/toast.md}
 */
export declare function useToaster<T>(toaster: ToasterStore<T>): () => ToastData<T>[];
//#endregion
//#region src/states/create-toggle-state.d.ts
interface ToggleStateControlledOptions {
  pressed: boolean;
  disabled?: boolean;
  onChange?: (state: boolean) => void;
}
interface ToggleStateUncontrolledOptions {
  defaultPressed: boolean;
  disabled?: boolean;
  onChange?: (state: boolean) => void;
}
type ToggleStateOptions = ToggleStateControlledOptions | ToggleStateUncontrolledOptions;
interface ToggleStateProperties {
  pressed: () => boolean;
  setState: (newState: boolean) => void;
  disabled: () => boolean;
  check: () => void;
  uncheck: () => void;
  toggle: () => void;
}
/**
 * Creates a pressed/unpressed state. Backs `Toggle`.
 *
 * Pass `defaultPressed` for uncontrolled state or `pressed` for controlled.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#toggle-state}
 */
export declare function createToggleState(options: ToggleStateOptions): ToggleStateProperties;
interface ToggleStateRenderProps {
  children?: JSX.Element | ((state: ToggleStateProperties) => JSX.Element);
}
/**
 * Reads the nearest toggle state from context. Throws when there is none.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#toggle-state}
 */
export declare function useToggleState(): ToggleStateProperties;
/**
 * Passes the nearest toggle state to a render prop. A function child is
 * treated as a render prop only when it declares exactly one parameter.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#toggle-state}
 */
export declare function ToggleStateChild(props: ToggleStateRenderProps): JSX.Element;
//#endregion
//#region src/components/toggle/index.d.ts
export type ToggleControlledBaseProps = Prettify<ToggleStateControlledOptions & ToggleStateRenderProps>;
export type ToggleControlledProps<T extends ValidConstructor = 'button'> = HeadlessPropsWithRef<T, OmitAndMerge<ToggleControlledBaseProps, ButtonProps<T>>>;
export type ToggleUncontrolledBaseProps = Prettify<ToggleStateUncontrolledOptions & ToggleStateRenderProps>;
export type ToggleUncontrolledProps<T extends ValidConstructor = 'button'> = HeadlessPropsWithRef<T, OmitAndMerge<ToggleUncontrolledBaseProps, ButtonProps<T>>>;
export type ToggleProps<T extends ValidConstructor = 'button'> = ToggleControlledProps<T> | ToggleUncontrolledProps<T>;
/**
 * A two-state button, pressed or unpressed, reported through `aria-pressed`.
 * Use it for controls that stay on until pressed again, such as bold in a text
 * editor.
 *
 * Renders a `<button>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/toggle.md}
 */
export declare function Toggle<T extends ValidConstructor = 'button'>(props: ToggleProps<T>): JSX.Element;
//#endregion
//#region src/components/toolbar/index.d.ts
export type ToolbarProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, {
  horizontal?: boolean;
}>;
/**
 * A group of controls that share one tab stop. The arrow keys move between
 * them, so a toolbar of ten buttons costs the keyboard user one `Tab` instead
 * of ten.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/toolbar.md}
 */
export declare function Toolbar<T extends ValidConstructor = 'div'>(props: ToolbarProps<T>): JSX.Element;
//#endregion
//#region src/states/create-transition-state.d.ts
/**
 * The class names for one transition, already split into lists.
 *
 * `enter` and `leave` carry the CSS `transition` or `animation` declaration and
 * stay on for the whole of their phase; the `*From` and `*To` pairs are the
 * start and end states swapped between them. `entered` is the resting state,
 * applied once entering has finished.
 */
interface TransitionClasses {
  enter: string[];
  enterFrom: string[];
  enterTo: string[];
  entered: string[];
  leave: string[];
  leaveFrom: string[];
  leaveTo: string[];
}
/**
 * Callbacks fired around a transition.
 *
 * A run that gets interrupted never reaches its `afterEnter` or `afterLeave`,
 * which is what keeps a caller from unmounting an element that is on its way
 * back in.
 */
interface TransitionHooks {
  /** Fired for every phase change, including the ones a caller cannot hook. */
  onTransition?: (state: TransitionStates) => void;
  beforeEnter?: () => void;
  afterEnter?: () => void;
  beforeLeave?: () => void;
  afterLeave?: () => void;
}
/** The phase a transition is in, published as the `tc-transition` attribute. */
type TransitionStates = 'enter-from' | 'enter-to' | 'entered' | 'leave-from' | 'leave-to';
/**
 * Runs one element's enter and leave transitions.
 *
 * The state holds no reactivity of its own: a caller feeds it an element and a
 * set of classes, calls {@link show} or {@link hide}, and observes progress
 * through {@link TransitionHooks}. That is what lets the same machinery drive
 * both a `<Transition>` and a `<TransitionChild>`.
 *
 * Each step waits on the element's running animations rather than on a
 * `transitionend` listener, so an element with nothing to animate simply moves
 * on to the next step instead of waiting for an event that never arrives.
 *
 * States nest: a parent enters before its children and leaves after them, so a
 * group animates in from the outside and out from the inside.
 */
export declare class TransitionState {
  visible: () => boolean;
  private readonly hooks;
  /**
   * @param visible Whether this state has finished entering. Children read it to
   * decide when they may mount.
   * @param hooks Called as the transition progresses.
   */
  constructor(visible: () => boolean, hooks: TransitionHooks);
  private readonly children;
  register(child: TransitionState): void;
  unregister(child: TransitionState): void;
  private element?;
  /**
   * The element to transition. It arrives after construction, because the
   * caller only has a ref once its element has rendered, and it changes again
   * whenever an `unmount`ing element is rebuilt.
   */
  setElement(element: HTMLElement): void;
  private classes?;
  /**
   * Classes are re-read on every transition rather than captured once, so
   * changing a class prop applies to the next transition instead of restarting
   * the current one.
   */
  setClasses(classes: TransitionClasses): void;
  /**
   * Bumped whenever a transition starts. A run whose token no longer matches
   * has been superseded by one going the other way, and stops at its next step
   * instead of finishing and undoing the newer transition.
   */
  private token;
  private showing?;
  private hiding?;
  /**
   * Enters, then lets the children enter behind it.
   *
   * Every wait is followed by a token check: if a leave has started in the
   * meantime, this run abandons its remaining steps rather than putting classes
   * back on an element that is now going the other way.
   */
  private _show;
  /**
   * Enters, interrupting a leave if one is running.
   *
   * Resolves once this element and everything nested inside it has entered, or
   * as soon as the run is superseded by a {@link hide}.
   */
  show(): Promise<void>;
  /**
   * Lets the children leave first, then leaves.
   *
   * Waiting for the children is what keeps a group together: the parent is
   * still on screen, and still animating, until the last thing inside it has
   * gone.
   */
  private _hide;
  /**
   * Leaves, interrupting an enter if one is running.
   *
   * Resolves once everything nested inside has left and this element has
   * finished its own leave, or as soon as the run is superseded by a
   * {@link show}.
   */
  hide(): Promise<void>;
}
//#endregion
//#region src/components/transition/index.d.ts
export interface TransitionRootBaseProps {
  show: boolean;
}
export interface TransitionBaseChildProps extends UnmountableProps, TransitionHooks {
  appear?: boolean;
  enter?: string;
  enterFrom?: string;
  enterTo?: string;
  entered?: string;
  leave?: string;
  leaveFrom?: string;
  leaveTo?: string;
}
export type TransitionChildProps<T extends ValidConstructor = 'div'> = HeadlessPropsWithRef<T, TransitionBaseChildProps>;
/**
 * A {@link Transition} that follows its parent transition instead of its own
 * `show` prop, so several elements can animate together on different timings.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/transition.md}
 */
export declare function TransitionChild<T extends ValidConstructor = 'div'>(props: TransitionChildProps<T>): JSX.Element;
export type TransitionProps<T extends ValidConstructor = 'div'> = Prettify<TransitionRootBaseProps & TransitionChildProps<T>>;
/**
 * Applies enter and leave classes around a `show` prop, and keeps its children
 * mounted until the leave transition finishes. It only adds and removes
 * classes; the animation itself is yours to write.
 *
 * Renders a `<div>` by default.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/components/transition.md}
 */
export declare function Transition<T extends ValidConstructor = 'div'>(props: TransitionProps<T>): JSX.Element;
//#endregion
//#region src/states/create-input-state.d.ts
interface InputStateControlledOptions {
  value: string | undefined;
  disabled?: boolean;
  onChange?: (state?: string) => void;
}
interface InputStateUncontrolledOptions {
  defaultValue: string | undefined;
  disabled?: boolean;
  onChange?: (state?: string) => void;
}
type InputStateOptions = InputStateControlledOptions | InputStateUncontrolledOptions;
interface InputStateProperties {
  value: () => string | undefined;
  setState: (newState?: string) => void;
  disabled: () => boolean;
}
/**
 * Creates a plain string state. Exported for building text-input components.
 *
 * Pass `defaultValue` for uncontrolled state or `value` for controlled.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#input-state}
 */
export declare function createInputState(options: InputStateOptions): InputStateProperties;
interface InputStateRenderProps {
  children?: JSX.Element | ((state: InputStateProperties) => JSX.Element);
}
interface InputStateProviderProps extends InputStateRenderProps {
  state: InputStateProperties;
}
/**
 * Publishes an input state to its descendants, so `useInputState` and
 * `InputStateChild` can reach it. No component in the library creates an input
 * state, so this is the only way to make one available to a subtree.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#input-state}
 */
export declare function InputStateProvider(props: InputStateProviderProps): JSX.Element;
/**
 * Reads the nearest input state from context. Throws when there is none.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#input-state}
 */
export declare function useInputState(): InputStateProperties;
/**
 * Passes the nearest input state to a render prop. A function child is treated
 * as a render prop only when it declares exactly one parameter.
 *
 * @see {@link https://github.com/lxsmnsyc/terracotta/blob/main/docs/states.md#input-state}
 */
export declare function InputStateChild(props: InputStateRenderProps): JSX.Element;
//#endregion
//#region src/utils/Fragment.d.ts
interface FragmentProps {
  children?: JSX.Element;
}
declare function Fragment(props: FragmentProps): JSX.Element;
//#endregion
export { type AutocompleteOptionStateOptions, type AutocompleteOptionStateProperties, type AutocompleteOptionStateRenderProps, type AutocompleteStateProperties, type AutocompleteStateRenderProps, type CheckStateControlledOptions, type CheckStateOptions, type CheckStateProperties, type CheckStateRenderProps, type CheckStateUncontrolledOptions, type DisclosureStateControlledOptions, type DisclosureStateOptions, type DisclosureStateProperties, type DisclosureStateRenderProps, type DisclosureStateUncontrolledOptions, Fragment, type FragmentProps, type InputStateControlledOptions, type InputStateOptions, type InputStateProperties, type InputStateProviderProps, type InputStateRenderProps, type InputStateUncontrolledOptions, type MultipleAutocompleteStateControlledOptions, type MultipleAutocompleteStateOptions, type MultipleAutocompleteStateUncontrolledOptions, type MultipleSelectStateControlledOptions, type MultipleSelectStateOptions, type MultipleSelectStateUncontrolledOptions, type SelectOptionStateOptions, type SelectOptionStateProperties, type SelectOptionStateRenderProps, type SelectStateProperties, type SelectStateRenderProps, type SingleAutocompleteStateControlledOptions, type SingleAutocompleteStateOptions, type SingleAutocompleteStateUncontrolledOptions, type SingleSelectStateControlledOptions, type SingleSelectStateOptions, type SingleSelectStateUncontrolledOptions, type ToggleStateControlledOptions, type ToggleStateOptions, type ToggleStateProperties, type ToggleStateRenderProps, type ToggleStateUncontrolledOptions, type TransitionClasses, type TransitionHooks, type TransitionStates };
//# sourceMappingURL=index.d.ts.map