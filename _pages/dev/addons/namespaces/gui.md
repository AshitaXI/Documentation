---
permalink: /dev/addons/namespaces/gui/
title: "Namespace: gui"
toc: true
---

The `gui` namespace contains functions that are used for working with Ashita's in-game GUI system. (Powered by ImGui)

This allows addons to create rich user interfaces.

You can access this namespace via:
```lua
ashita.gui.
```

Because of the nature of these functions and the amount of functions that exist, I do not plan to create full documentation for each function. You can find an example of the ImGui demo application ported to an Ashita addon here instead.

This will serve as a demo of how to use these functions:
[https://gist.github.com/atom0s/188283e6ff097f37fa31400f22ec8762](https://gist.github.com/atom0s/188283e6ff097f37fa31400f22ec8762)

In order to make use of the GUI features properly, your addon should require the imguidef library via:
```lua
require 'imguidef';
```

By including this helper file, this also exposes these GUI functions via a global 'imgui'. Instead of having to use 'ashita.gui.' before every call, instead you just need to use 'imgui.' instead. For example:
```lua
-- before
local hide = ashita.gui.GetHide();
 
-- after
local hide = imgui.GetHide();
```

Most of the calls are straight-forward and used as they are in C++. However, some of them had to have minor changes to work with Lua's types and lack of pointers. The following is a list of how things are implemented.

Please note, the following changes apply to ALL functions listed below: 

  * Any function that takes ImVec2(…) is replaced by two float values instead.
  * Any function that takes ImVec4(…) is replaced by four float values instead.
    * _**Example (Before):** void SetNextWindowPos(const ImVec2& pos, ImGuiSetCond cond = 0);_
    * _**Example (After):** void SetNextWindowPos(float pos_x, float pos_y, ImGuiSetCond cond = 0);_
  * Any function that returns ImVec2(…) instead returns two values.
  * Any function that returns ImVec4(…) instead returns four values.
    * _**Example (Before):** ImVec2 GetWindowPos(void);_
    * _**Example (After):** pos_x, pos_y = GetWindowPos();_
  * Any function that takes a pointer value is replaced with an ImGuiVar variable instead. (See more info on ImGuiVar below.)
  * Any function that accepts varargs '…' are not handled as such. Instead they accept only a single string. Use Lua's   * buildt-in string.format function to format strings.
  * Any function that accepts va_list as an argument type is not implemented as Lua has no way to do this natively.

---

  * <span style="color: #62c462">bool GetHideObjects(void) const;</span>
  * <span style="color: #62c462">void SetHideObjects(bool bHide);</span>
    * Implemented as 'imgui.GetHide()' and 'imgui.SetHide(hide)'.
  * <span style="color: #d35547">ImGuiIO& GetIO(void);</span>
  * <span style="color: #d35547">ImGuiStyle& GetStyle(void);</span>
  * <span style="color: #d35547">ImDrawData* GetDrawData(void);</span>
    * Not implemented through these functions.
    * GetIO can be accessed via 'imgui.io'.
    * GetStyle can be accessed via 'imgui.style'.
    * GetDrawData is not implemented at all currently.
  * <span style="color: #62c462">void ShowUserGuide(void);</span>
  * <span style="color: #62c462">void ShowStyleEditor(ImGuiStyle* ref = NULL);</span>
  * <span style="color: #62c462">void ShowTestWindow(bool* p_open = NULL);</span>
  * <span style="color: #62c462">void ShowMetricsWindow(bool* p_open = NULL);</span>
  * <span style="color: #62c462">bool Begin(const char* name, bool* p_open = NULL, ImGuiWindowFlags flags = 0);</span>
  * <span style="color: #62c462">bool Begin(const char* name, bool* p_open, const ImVec2& size_on_first_use, float bg_alpha = -1.0f, ImGuiWindowFlags flags = 0);</span>
  * <span style="color: #62c462">void End(void);</span>
  * <span style="color: #62c462">bool BeginChild(const char* str_id, const ImVec2& size = ImVec2(0, 0), bool border = false, ImGuiWindowFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool BeginChild(ImGuiID id, const ImVec2& size = ImVec2(0, 0), bool border = false, ImGuiWindowFlags extra_flags = 0);</span>
  * <span style="color: #62c462">void EndChild(void);</span>
  * <span style="color: #62c462">ImVec2 GetContentRegionMax(void);</span>
  * <span style="color: #62c462">ImVec2 GetContentRegionAvail(void);</span>
  * <span style="color: #62c462">float GetContentRegionAvailWidth(void);</span>
  * <span style="color: #62c462">ImVec2 GetWindowContentRegionMin(void);</span>
  * <span style="color: #62c462">ImVec2 GetWindowContentRegionMax(void);</span>
  * <span style="color: #62c462">float GetWindowContentRegionWidth(void);</span>
  * <span style="color: #d35547">ImDrawList* GetWindowDrawList(void);</span>
  * <span style="color: #62c462">ImVec2 GetWindowPos(void);</span>
  * <span style="color: #62c462">ImVec2 GetWindowSize(void);</span>
  * <span style="color: #62c462">float GetWindowWidth(void);</span>
  * <span style="color: #62c462">float GetWindowHeight(void);</span>
  * <span style="color: #62c462">bool IsWindowCollapsed(void);</span>
  * <span style="color: #62c462">void SetWindowFontScale(float scale);</span>
  * <span style="color: #62c462">void SetNextWindowPos(const ImVec2& pos, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetNextWindowPosCenter(ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetNextWindowSize(const ImVec2& size, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetNextWindowSizeConstraints(const ImVec2& size_min, const ImVec2& size_max, ImGuiSizeConstraintCallback custom_callback = NULL, void* custom_callback_data = NULL);</span>
    * callback is implemented as a string. It is the name to a Lua function to call when the callback is invoked. (custom_callback_data is not implemented.)
  * <span style="color: #62c462">void SetNextWindowContentSize(const ImVec2& size);</span>
  * <span style="color: #62c462">void SetNextWindowContentWidth(float width);</span>
  * <span style="color: #62c462">void SetNextWindowCollapsed(bool collapsed, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetNextWindowFocus(void);</span>
  * <span style="color: #62c462">void SetWindowPos(const ImVec2& pos, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetWindowSize(const ImVec2& size, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetWindowCollapsed(bool collapsed, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetWindowFocus(void);</span>
  * <span style="color: #62c462">void SetWindowPos(const char* name, const ImVec2& pos, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetWindowSize(const char* name, const ImVec2& size, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetWindowCollapsed(const char* name, bool collapsed, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">void SetWindowFocus(const char* name);</span>
  * <span style="color: #62c462">float GetScrollX(void);</span>
  * <span style="color: #62c462">float GetScrollY(void);</span>
  * <span style="color: #62c462">float GetScrollMaxX(void);</span>
  * <span style="color: #62c462">float GetScrollMaxY(void);</span>
  * <span style="color: #62c462">void SetScrollX(float scroll_x);</span>
  * <span style="color: #62c462">void SetScrollY(float scroll_y);</span>
  * <span style="color: #62c462">void SetScrollHere(float center_y_ratio = 0.5f);</span>
  * <span style="color: #62c462">void SetScrollFromPosY(float pos_y, float center_y_ratio = 0.5f);</span>
  * <span style="color: #62c462">void SetKeyboardFocusHere(int offset = 0);</span>
  * <span style="color: #d35547">void SetStateStorage(ImGuiStorage* tree);</span>
  * <span style="color: #d35547">ImGuiStorage* GetStateStorage(void);</span>
  * <span style="color: #62c462">void PushFont(ImFont* font);</span>
  * <span style="color: #62c462">void PopFont(void);</span>
  * <span style="color: #62c462">void PushStyleColor(ImGuiCol idx, const ImVec4& col);</span>
  * <span style="color: #62c462">void PopStyleColor(int count = 1);</span>
  * <span style="color: #62c462">void PushStyleVar(ImGuiStyleVar idx, float val);</span>
  * <span style="color: #62c462">void PushStyleVar(ImGuiStyleVar idx, const ImVec2& val);</span>
  * <span style="color: #62c462">void PopStyleVar(int count = 1);</span>
  * <span style="color: #d35547">ImFont* GetFont(void);</span>
  * <span style="color: #62c462">float GetFontSize(void);</span>
  * <span style="color: #62c462">ImVec2 GetFontTexUvWhitePixel(void);</span>
  * <span style="color: #62c462">ImU32 GetColorU32(ImGuiCol idx, float alpha_mul = 1.0f);</span>
  * <span style="color: #62c462">ImU32 GetColorU32(const ImVec4& col);</span>
  * <span style="color: #62c462">void PushItemWidth(float item_width);</span>
  * <span style="color: #62c462">void PopItemWidth(void);</span>
  * <span style="color: #62c462">float CalcItemWidth(void);</span>
  * <span style="color: #62c462">void PushTextWrapPos(float wrap_pos_x = 0.0f);</span>
  * <span style="color: #62c462">void PopTextWrapPos(void);</span>
  * <span style="color: #62c462">void PushAllowKeyboardFocus(bool v);</span>
  * <span style="color: #62c462">void PopAllowKeyboardFocus(void);</span>
  * <span style="color: #62c462">void PushButtonRepeat(bool repeat);</span>
  * <span style="color: #62c462">void PopButtonRepeat(void);</span>
  * <span style="color: #62c462">void Separator(void);</span>
  * <span style="color: #62c462">void SameLine(float pos_x = 0.0f, float spacing_w = -1.0f);</span>
  * <span style="color: #62c462">void NewLine(void);</span>
  * <span style="color: #62c462">void Spacing(void);</span>
  * <span style="color: #62c462">void Dummy(const ImVec2& size);</span>
  * <span style="color: #62c462">void Indent(float indent_w = 0.0f);</span>
  * <span style="color: #62c462">void Unindent(float indent_w = 0.0f);</span>
  * <span style="color: #62c462">void BeginGroup(void);</span>
  * <span style="color: #62c462">void EndGroup(void);</span>
  * <span style="color: #62c462">ImVec2 GetCursorPos(void);</span>
  * <span style="color: #62c462">float GetCursorPosX(void);</span>
  * <span style="color: #62c462">float GetCursorPosY(void);</span>
  * <span style="color: #62c462">void SetCursorPos(const ImVec2& local_pos);</span>
  * <span style="color: #62c462">void SetCursorPosX(float x);</span>
  * <span style="color: #62c462">void SetCursorPosY(float y);</span>
  * <span style="color: #62c462">ImVec2 GetCursorStartPos(void);</span>
  * <span style="color: #62c462">ImVec2 GetCursorScreenPos(void);</span>
  * <span style="color: #62c462">void SetCursorScreenPos(const ImVec2& pos);</span>
  * <span style="color: #62c462">void AlignFirstTextHeightToWidgets(void);</span>
  * <span style="color: #62c462">float GetTextLineHeight(void);</span>
  * <span style="color: #62c462">float GetTextLineHeightWithSpacing(void);</span>
  * <span style="color: #62c462">float GetItemsLineHeightWithSpacing(void);</span>
  * <span style="color: #62c462">void Columns(int count = 1, const char* id = NULL, bool border = true);</span>
  * <span style="color: #62c462">void NextColumn(void);</span>
  * <span style="color: #62c462">int GetColumnIndex(void);</span>
  * <span style="color: #62c462">float GetColumnOffset(int column_index = -1);</span>
  * <span style="color: #62c462">void SetColumnOffset(int column_index, float offset_x);</span>
  * <span style="color: #62c462">float GetColumnWidth(int column_index = -1);</span>
  * <span style="color: #62c462">int GetColumnsCount(void);</span>
  * <span style="color: #62c462">void PushID(const char* str_id);</span>
  * <span style="color: #62c462">void PushID(const char* str_id_begin, const char* str_id_end);</span>
  * <span style="color: #62c462">void PushID(const void* ptr_id);</span>
  * <span style="color: #62c462">void PushID(int int_id);</span>
  * <span style="color: #62c462">void PopID(void);</span>
  * <span style="color: #62c462">ImGuiID GetID(const char* str_id);</span>
  * <span style="color: #62c462">ImGuiID GetID(const char* str_id_begin, const char* str_id_end);</span>
  * <span style="color: #62c462">ImGuiID GetID(const void* ptr_id);</span>
  * <span style="color: #62c462">void Text(const char* fmt, ...);</span>
  * <span style="color: #d35547">void TextV(const char* fmt, va_list args);</span>
  * <span style="color: #62c462">void TextColored(const ImVec4& col, const char* fmt, ...);</span>
  * <span style="color: #d35547">void TextColoredV(const ImVec4& col, const char* fmt, va_list args);</span>
  * <span style="color: #62c462">void TextDisabled(const char* fmt, ...);</span>
  * <span style="color: #d35547">void TextDisabledV(const char* fmt, va_list args);</span>
  * <span style="color: #62c462">void TextWrapped(const char* fmt, ...);</span>
  * <span style="color: #d35547">void TextWrappedV(const char* fmt, va_list args);</span>
  * <span style="color: #62c462">void TextUnformatted(const char* text, const char* text_end = NULL);</span>
    * There may be some issues with this function. It may change in the future.
  * <span style="color: #62c462">void LabelText(const char* label, const char* fmt, ...);</span>
  * <span style="color: #d35547">void LabelTextV(const char* label, const char* fmt, va_list args);</span>
  * <span style="color: #62c462">void Bullet(void);</span>
  * <span style="color: #62c462">void BulletText(const char* fmt, ...);</span>
  * <span style="color: #d35547">void BulletTextV(const char* fmt, va_list args);</span>
  * <span style="color: #62c462">bool Button(const char* label, const ImVec2& size = ImVec2(0, 0));</span>
  * <span style="color: #62c462">bool SmallButton(const char* label);</span>
  * <span style="color: #62c462">bool InvisibleButton(const char* str_id, const ImVec2& size);</span>
  * <span style="color: #62c462">void Image(ImTextureID user_texture_id, const ImVec2& size, const ImVec2& uv0 = ImVec2(0, 0), const ImVec2& uv1 = ImVec2(1, 1), const ImVec4& tint_col = ImVec4(1, 1, 1, 1), const ImVec4& border_col = ImVec4(0, 0, 0, 0));</span>
  * <span style="color: #62c462">bool ImageButton(ImTextureID user_texture_id, const ImVec2& size, const ImVec2& uv0 = ImVec2(0, 0), const ImVec2& uv1 = ImVec2(1, 1), int frame_padding = -1, const ImVec4& bg_col = ImVec4(0, 0, 0, 0), const ImVec4& tint_col = ImVec4(1, 1, 1, 1));</span>
  * <span style="color: #62c462">bool Checkbox(const char* label, bool* v);</span>
  * <span style="color: #62c462">bool CheckboxFlags(const char* label, unsigned int* flags, unsigned int flags_value);</span>
  * <span style="color: #62c462">bool RadioButton(const char* label, bool active);</span>
  * <span style="color: #62c462">bool RadioButton(const char* label, int* v, int v_button);</span>
  * <span style="color: #d35547">bool Combo(const char* label, int* current_item, const char%%**%% items, int items_count, int height_in_items = -1);</span>
  * <span style="color: #62c462">bool Combo(const char* label, int* current_item, const char* items_separated_by_zeros, int height_in_items = -1);</span>
  * <span style="color: #d35547">bool Combo(const char* label, int* current_item, bool(*items_getter)(void* data, int idx, const char%%**%% out_text), void* data, int items_count, int height_in_items = -1);</span>
  * <span style="color: #62c462">bool ColorButton(const ImVec4& col, bool small_height = false, bool outline_border = true);</span>
  * <span style="color: #62c462">bool ColorEdit3(const char* label, float col[3]);</span>
  * <span style="color: #62c462">bool ColorEdit4(const char* label, float col[4], bool show_alpha = true);</span>
  * <span style="color: #62c462">void ColorEditMode(ImGuiColorEditMode mode);</span>
  * <span style="color: #62c462">void PlotLines(const char* label, const float* values, int values_count, int values_offset = 0, const char* overlay_text = NULL, float scale_min = FLT_MAX, float scale_max = FLT_MAX, ImVec2 graph_size = ImVec2(0, 0), int stride = sizeof(float));</span>
    * Implemented in a custom manner to support an array of  float values, using a Lua table. Call is setup as:
      * imgui.PlotLines(label, values_table, values_count, values_offset, overlay_text, scale_min, scale_max, graph_size_x, graph_size_y, stride);
      * Default values are still present starting at values_offset.
  * <span style="color: #d35547">void PlotLines(const char* label, float(*values_getter)(void* data, int idx), void* data, int values_count, int values_offset = 0, const char* overlay_text = NULL, float scale_min = FLT_MAX, float scale_max = FLT_MAX, ImVec2 graph_size = ImVec2(0, 0));</span>
  * <span style="color: #62c462">void PlotHistogram(const char* label, const float* values, int values_count, int values_offset = 0, const char* overlay_text = NULL, float scale_min = FLT_MAX, float scale_max = FLT_MAX, ImVec2 graph_size = ImVec2(0, 0), int stride = sizeof(float));</span>
    * Implemented in a custom manner to support an array of  float values, using a Lua table. Call is setup as:
      * imgui.PlotHistogram(label, values_table, values_count, values_offset, overlay_text, scale_min, scale_max, graph_size_x, graph_size_y, stride);
      * Default values are still present starting at values_offset.
  * <span style="color: #d35547">void PlotHistogram(const char* label, float(*values_getter)(void* data, int idx), void* data, int values_count, int values_offset = 0, const char* overlay_text = NULL, float scale_min = FLT_MAX, float scale_max = FLT_MAX, ImVec2 graph_size = ImVec2(0, 0));</span>
  * <span style="color: #62c462">void ProgressBar(float fraction, const ImVec2& size_arg = ImVec2(-1, 0), const char* overlay = NULL);</span>
  * <span style="color: #62c462">bool DragFloat(const char* label, float* v, float v_speed = 1.0f, float v_min = 0.0f, float v_max = 0.0f, const char* display_format = "%.3f", float power = 1.0f);</span>
  * <span style="color: #62c462">bool DragFloat2(const char* label, float v[2], float v_speed = 1.0f, float v_min = 0.0f, float v_max = 0.0f, const char* display_format = "%.3f", float power = 1.0f);</span>
  * <span style="color: #62c462">bool DragFloat3(const char* label, float v[3], float v_speed = 1.0f, float v_min = 0.0f, float v_max = 0.0f, const char* display_format = "%.3f", float power = 1.0f);</span>
  * <span style="color: #62c462">bool DragFloat4(const char* label, float v[4], float v_speed = 1.0f, float v_min = 0.0f, float v_max = 0.0f, const char* display_format = "%.3f", float power = 1.0f);</span>
  * <span style="color: #62c462">bool DragFloatRange2(const char* label, float* v_current_min, float* v_current_max, float v_speed = 1.0f, float v_min = 0.0f, float v_max = 0.0f, const char* display_format = "%.3f", const char* display_format_max = NULL, float power = 1.0f);</span>
  * <span style="color: #62c462">bool DragInt(const char* label, int* v, float v_speed = 1.0f, int v_min = 0, int v_max = 0, const char* display_format = "%.0f");</span>
  * <span style="color: #62c462">bool DragInt2(const char* label, int v[2], float v_speed = 1.0f, int v_min = 0, int v_max = 0, const char* display_format = "%.0f");</span>
  * <span style="color: #62c462">bool DragInt3(const char* label, int v[3], float v_speed = 1.0f, int v_min = 0, int v_max = 0, const char* display_format = "%.0f");</span>
  * <span style="color: #62c462">bool DragInt4(const char* label, int v[4], float v_speed = 1.0f, int v_min = 0, int v_max = 0, const char* display_format = "%.0f");</span>
  * <span style="color: #62c462">bool DragIntRange2(const char* label, int* v_current_min, int* v_current_max, float v_speed = 1.0f, int v_min = 0, int v_max = 0, const char* display_format = "%.0f", const char* display_format_max = NULL);</span>
  * <span style="color: #62c462">bool InputText(const char* label, char* buf, size_t buf_size, ImGuiInputTextFlags flags = 0, ImGuiTextEditCallback callback = NULL, void* user_data = NULL);</span>
    * callback is implemented as a string. It is the name to a Lua function to call when the callback is invoked. (user_data is not implemented.)
  * <span style="color: #62c462">bool InputTextMultiline(const char* label, char* buf, size_t buf_size, const ImVec2& size = ImVec2(0, 0), ImGuiInputTextFlags flags = 0, ImGuiTextEditCallback callback = NULL, void* user_data = NULL);</span>
    * callback is implemented as a string. It is the name to a Lua function to call when the callback is invoked. (user_data is not implemented.)
  * <span style="color: #62c462">bool InputFloat(const char* label, float* v, float step = 0.0f, float step_fast = 0.0f, int decimal_precision = -1, ImGuiInputTextFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool InputFloat2(const char* label, float v[2], int decimal_precision = -1, ImGuiInputTextFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool InputFloat3(const char* label, float v[3], int decimal_precision = -1, ImGuiInputTextFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool InputFloat4(const char* label, float v[4], int decimal_precision = -1, ImGuiInputTextFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool InputInt(const char* label, int* v, int step = 1, int step_fast = 100, ImGuiInputTextFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool InputInt2(const char* label, int v[2], ImGuiInputTextFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool InputInt3(const char* label, int v[3], ImGuiInputTextFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool InputInt4(const char* label, int v[4], ImGuiInputTextFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool SliderFloat(const char* label, float* v, float v_min, float v_max, const char* display_format = "%.3f", float power = 1.0f);</span>
  * <span style="color: #62c462">bool SliderFloat2(const char* label, float v[2], float v_min, float v_max, const char* display_format = "%.3f", float power = 1.0f);</span>
  * <span style="color: #62c462">bool SliderFloat3(const char* label, float v[3], float v_min, float v_max, const char* display_format = "%.3f", float power = 1.0f);</span>
  * <span style="color: #62c462">bool SliderFloat4(const char* label, float v[4], float v_min, float v_max, const char* display_format = "%.3f", float power = 1.0f);</span>
  * <span style="color: #62c462">bool SliderAngle(const char* label, float* v_rad, float v_degrees_min = -360.0f, float v_degrees_max = +360.0f);</span>
  * <span style="color: #62c462">bool SliderInt(const char* label, int* v, int v_min, int v_max, const char* display_format = "%.0f");</span>
  * <span style="color: #62c462">bool SliderInt2(const char* label, int v[2], int v_min, int v_max, const char* display_format = "%.0f");</span>
  * <span style="color: #62c462">bool SliderInt3(const char* label, int v[3], int v_min, int v_max, const char* display_format = "%.0f");</span>
  * <span style="color: #62c462">bool SliderInt4(const char* label, int v[4], int v_min, int v_max, const char* display_format = "%.0f");</span>
  * <span style="color: #62c462">bool VSliderFloat(const char* label, const ImVec2& size, float* v, float v_min, float v_max, const char* display_format = "%.3f", float power = 1.0f);</span>
  * <span style="color: #62c462">bool VSliderInt(const char* label, const ImVec2& size, int* v, int v_min, int v_max, const char* display_format = "%.0f");</span>
  * <span style="color: #62c462">bool TreeNode(const char* label);</span>
  * <span style="color: #62c462">bool TreeNode(const char* str_id, const char* fmt, ...);</span>
  * <span style="color: #62c462">bool TreeNode(const void* ptr_id, const char* fmt, ...);</span>
  * <span style="color: #d35547">bool TreeNodeV(const char* str_id, const char* fmt, va_list args);</span>
  * <span style="color: #d35547">bool TreeNodeV(const void* ptr_id, const char* fmt, va_list args);</span>
  * <span style="color: #62c462">bool TreeNodeEx(const char* label, ImGuiTreeNodeFlags flags = 0);</span>
  * <span style="color: #62c462">bool TreeNodeEx(const char* str_id, ImGuiTreeNodeFlags flags, const char* fmt, ...);</span>
  * <span style="color: #62c462">bool TreeNodeEx(const void* ptr_id, ImGuiTreeNodeFlags flags, const char* fmt, ...);</span>
  * <span style="color: #d35547">bool TreeNodeExV(const char* str_id, ImGuiTreeNodeFlags flags, const char* fmt, va_list args);</span>
  * <span style="color: #d35547">bool TreeNodeExV(const void* ptr_id, ImGuiTreeNodeFlags flags, const char* fmt, va_list args);</span>
  * <span style="color: #62c462">void TreePush(const char* str_id = NULL);</span>
  * <span style="color: #62c462">void TreePush(const void* ptr_id = NULL);</span>
  * <span style="color: #62c462">void TreePop(void);</span>
  * <span style="color: #62c462">void TreeAdvanceToLabelPos(void);</span>
  * <span style="color: #62c462">float GetTreeNodeToLabelSpacing(void);</span>
  * <span style="color: #62c462">void SetNextTreeNodeOpen(bool is_open, ImGuiSetCond cond = 0);</span>
  * <span style="color: #62c462">bool CollapsingHeader(const char* label, ImGuiTreeNodeFlags flags = 0);</span>
  * <span style="color: #62c462">bool CollapsingHeader(const char* label, bool* p_open, ImGuiTreeNodeFlags flags = 0);</span>
  * <span style="color: #62c462">bool Selectable(const char* label, bool selected = false, ImGuiSelectableFlags flags = 0, const ImVec2& size = ImVec2(0, 0));</span>
  * <span style="color: #62c462">bool Selectable(const char* label, bool* p_selected, ImGuiSelectableFlags flags = 0, const ImVec2& size = ImVec2(0, 0));</span>
  * <span style="color: #d35547">bool ListBox(const char* label, int* current_item, const char%%**%% items, int items_count, int height_in_items = -1);</span>
  * <span style="color: #62c462">bool ListBox(const char* label, int* current_item, const char* items_separated_by_zeros, int height_in_items = -1);</span>
  * <span style="color: #d35547">bool ListBox(const char* label, int* current_item, bool(*items_getter)(void* data, int idx, const char%%**%% out_text), void* data, int items_count, int height_in_items = -1);</span>
  * <span style="color: #62c462">bool ListBoxHeader(const char* label, const ImVec2& size = ImVec2(0, 0));</span>
  * <span style="color: #62c462">bool ListBoxHeader(const char* label, int items_count, int height_in_items = -1);</span>
  * <span style="color: #62c462">void ListBoxFooter(void);</span>
  * <span style="color: #62c462">void Value(const char* prefix, bool b);</span>
  * <span style="color: #62c462">void Value(const char* prefix, int v);</span>
  * <span style="color: #62c462">void Value(const char* prefix, unsigned int v);</span>
  * <span style="color: #62c462">void Value(const char* prefix, float v, const char* float_format = NULL);</span>
    * Value functions take an extra argument due to not being able to differentiate between the types in Lua.
      * Value(prefix, type, b);
      * Value(prefix, type, v);
      * Value(prefix, type, v);
      * Value(prefix, type, v, float_format);
        * Type: 0 = bool
        * Type: 1 = int
        * Type: 2 = unsigned int
        * Type: 3 = float
  * <span style="color: #62c462">void ValueColor(const char* prefix, const ImVec4& v);</span>
  * <span style="color: #62c462">void ValueColor(const char* prefix, unsigned int v);</span>
  * <span style="color: #62c462">void SetTooltip(const char* fmt, ...);</span>
  * <span style="color: #d35547">void SetTooltipV(const char* fmt, va_list args);</span>
  * <span style="color: #62c462">void BeginTooltip(void);</span>
  * <span style="color: #62c462">void EndTooltip(void);</span>
  * <span style="color: #62c462">bool BeginMainMenuBar(void);</span>
  * <span style="color: #62c462">void EndMainMenuBar(void);</span>
  * <span style="color: #62c462">bool BeginMenuBar(void);</span>
  * <span style="color: #62c462">void EndMenuBar(void);</span>
  * <span style="color: #62c462">bool BeginMenu(const char* label, bool enabled = true);</span>
  * <span style="color: #62c462">void EndMenu(void);</span>
  * <span style="color: #62c462">bool MenuItem(const char* label, const char* shortcut = NULL, bool selected = false, bool enabled = true);</span>
  * <span style="color: #62c462">bool MenuItem(const char* label, const char* shortcut, bool* p_selected, bool enabled = true);</span>
  * <span style="color: #62c462">void OpenPopup(const char* str_id);</span>
  * <span style="color: #62c462">bool BeginPopup(const char* str_id);</span>
  * <span style="color: #62c462">bool BeginPopupModal(const char* name, bool* p_open = NULL, ImGuiWindowFlags extra_flags = 0);</span>
  * <span style="color: #62c462">bool BeginPopupContextItem(const char* str_id, int mouse_button = 1);</span>
  * <span style="color: #62c462">bool BeginPopupContextWindow(bool also_over_items = true, const char* str_id = NULL, int mouse_button = 1);</span>
  * <span style="color: #62c462">bool BeginPopupContextVoid(const char* str_id = NULL, int mouse_button = 1);</span>
  * <span style="color: #62c462">void EndPopup(void);</span>
  * <span style="color: #62c462">void CloseCurrentPopup(void);</span>
  * <span style="color: #62c462">void LogToTTY(int max_depth = -1);</span>
  * <span style="color: #62c462">void LogToFile(int max_depth = -1, const char* filename = NULL);</span>
  * <span style="color: #62c462">void LogToClipboard(int max_depth = -1);</span>
  * <span style="color: #62c462">void LogFinish(void);</span>
  * <span style="color: #62c462">void LogButtons(void);</span>
  * <span style="color: #62c462">void LogText(const char* fmt, ...);</span>
    * These logging functions should not be relied on, they may be removed in the future.
  * <span style="color: #62c462">void PushClipRect(const ImVec2& clip_rect_min, const ImVec2& clip_rect_max, bool intersect_with_current_clip_rect);</span>
  * <span style="color: #62c462">void PopClipRect(void);</span>
  * <span style="color: #62c462">bool IsItemHovered(void);</span>
  * <span style="color: #62c462">bool IsItemHoveredRect(void);</span>
  * <span style="color: #62c462">bool IsItemActive(void);</span>
  * <span style="color: #62c462">bool IsItemClicked(int mouse_button = 0);</span>
  * <span style="color: #62c462">bool IsItemVisible(void);</span>
  * <span style="color: #62c462">bool IsAnyItemHovered(void);</span>
  * <span style="color: #62c462">bool IsAnyItemActive(void);</span>
  * <span style="color: #62c462">ImVec2 GetItemRectMin(void);</span>
  * <span style="color: #62c462">ImVec2 GetItemRectMax(void);</span>
  * <span style="color: #62c462">ImVec2 GetItemRectSize(void);</span>
  * <span style="color: #62c462">void SetItemAllowOverlap(void);</span>
  * <span style="color: #62c462">bool IsWindowHovered(void);</span>
  * <span style="color: #62c462">bool IsWindowFocused(void);</span>
  * <span style="color: #62c462">bool IsRootWindowFocused(void);</span>
  * <span style="color: #62c462">bool IsRootWindowOrAnyChildFocused(void);</span>
  * <span style="color: #62c462">bool IsRootWindowOrAnyChildHovered(void);</span>
  * <span style="color: #62c462">bool IsRectVisible(const ImVec2& size);</span>
  * <span style="color: #62c462">bool IsPosHoveringAnyWindow(const ImVec2& pos);</span>
  * <span style="color: #62c462">float GetTime(void);</span>
  * <span style="color: #62c462">int GetFrameCount(void);</span>
  * <span style="color: #62c462">const char* GetStyleColName(ImGuiCol idx);</span>
  * <span style="color: #d35547">ImVec2 CalcItemRectClosestPoint(const ImVec2& pos, bool on_edge = false, float outward = +0.0f);</span>
    * Not implementing this unless its requested.
  * <span style="color: #d35547">ImVec2 CalcTextSize(const char* text, const char* text_end = NULL, bool hide_text_after_double_hash = false, float wrap_width = -1.0f);</span>
    * Not implementing this unless it's requested.
  * <span style="color: #d35547">void CalcListClipping(int items_count, float items_height, int* out_items_display_start, int* out_items_display_end);</span>
    * Not implementing this unless it's requested.
  * <span style="color: #62c462">bool BeginChildFrame(ImGuiID id, const ImVec2& size, ImGuiWindowFlags extra_flags = 0);</span>
  * <span style="color: #62c462">void EndChildFrame(void);</span>
  * <span style="color: #62c462">ImVec4 ColorConvertU32ToFloat4(ImU32 in);</span>
  * <span style="color: #62c462">ImU32 ColorConvertFloat4ToU32(const ImVec4& in);</span>
  * <span style="color: #62c462">void ColorConvertRGBtoHSV(float r, float g, float b, float& out_h, float& out_s, float& out_v);</span>
    * Lua does not support 'out' values, instead, this function will return out_h, out_s, out_v.
  * <span style="color: #62c462">void ColorConvertHSVtoRGB(float h, float s, float v, float& out_r, float& out_g, float& out_b);</span>
    * Lua does not support 'out' values, instead, this function will return out_r, out_g, out_b.
  * <span style="color: #62c462">int GetKeyIndex(ImGuiKey key);</span>
  * <span style="color: #62c462">bool IsKeyDown(int key_index);</span>
  * <span style="color: #62c462">bool IsKeyPressed(int key_index, bool repeat = true);</span>
  * <span style="color: #62c462">bool IsKeyReleased(int key_index);</span>
  * <span style="color: #62c462">bool IsMouseDown(int button);</span>
  * <span style="color: #62c462">bool IsMouseClicked(int button, bool repeat = false);</span>
  * <span style="color: #62c462">bool IsMouseDoubleClicked(int button);</span>
  * <span style="color: #62c462">bool IsMouseReleased(int button);</span>
  * <span style="color: #62c462">bool IsMouseHoveringWindow(void);</span>
  * <span style="color: #62c462">bool IsMouseHoveringAnyWindow(void);</span>
  * <span style="color: #62c462">bool IsMouseHoveringRect(const ImVec2& r_min, const ImVec2& r_max, bool clip = true);</span>
  * <span style="color: #62c462">bool IsMouseDragging(int button = 0, float lock_threshold = -1.0f);</span>
  * <span style="color: #62c462">ImVec2 GetMousePos(void);</span>
  * <span style="color: #62c462">ImVec2 GetMousePosOnOpeningCurrentPopup(void);</span>
  * <span style="color: #62c462">ImVec2 GetMouseDragDelta(int button = 0, float lock_threshold = -1.0f);</span>
  * <span style="color: #62c462">void ResetMouseDragDelta(int button = 0);</span>
  * <span style="color: #62c462">ImGuiMouseCursor GetMouseCursor(void);</span>
  * <span style="color: #62c462">void SetMouseCursor(ImGuiMouseCursor type);</span>
  * <span style="color: #62c462">void CaptureKeyboardFromApp(bool capture = true);</span>
  * <span style="color: #62c462">void CaptureMouseFromApp(bool capture = true);</span>
  * <span style="color: #d35547">void* MemAlloc(size_t sz);</span>
    * Not implementing this function.
  * <span style="color: #d35547">void MemFree(void* ptr);</span>
    * Not implementing this function.
  * <span style="color: #62c462">const char* GetClipboardText(void);</span>
  * <span style="color: #62c462">void SetClipboardText(const char* text);</span>
  * <span style="color: #62c462">const char* GetVersion(void);</span>
  * <span style="color: #d35547">ImGuiContext* CreateContext(void* (*malloc_fn)(size_t) = NULL, void(*free_fn)(void*) = NULL);</span>
    * Not implementing this function.
  * <span style="color: #d35547">void DestroyContext(ImGuiContext* ctx);</span>
    * Not implementing this function.
  * <span style="color: #d35547">ImGuiContext* GetCurrentContext(void);</span>
    * Not implementing this function.
  * <span style="color: #d35547">void SetCurrentContext(ImGuiContext* ctx);</span>
    * Not implementing this function.

## Notes

**InputText / InputTextMultiline** - The callback, if present, should be a string that points to a callback function like this:
  * The callbacks data is a imgui.ImGuiTextEditCallbackData structure instance.

```lua
if (imgui.InputText('test', test_text_input_buffer, 1024, imgui.bor(ImGuiInputTextFlags_EnterReturnsTrue,ImGuiInputTextFlags_CallbackCompletion,ImGuiInputTextFlags_CallbackHistory), 'test_callback')) then
    print('Enter was pressed!');
end
     
function test_callback(data)
    print('Callback was fired!');
    return 0;
end
```

**SetNextWindowSizeConstraints** - The callback, if present, should be a string that points to a callback function like this: 
  * The callbacks data is a imgui.ImGuiSizeConstraintCallbackData structure instance.

```lua
function SquareResizeConstraint(data)
    data.DesiredSize = ImVec2(math.max(data.DesiredSize.x, data.DesiredSize.y), math.max(data.DesiredSize.x, data.DesiredSize.y));    
end
 
imgui.SetNextWindowSizeConstraints(0, 0, float_max, float_max, 'SquareResizeConstraint');
```

---

## ImGuiSizeConstraintCallbackData

The ImGuiSizeConstraintCallbackData structure contains information used for window resizing callbacks. This allows users to adjust how their window(s) resize if they want to use certain constraints.

The following data is exposed in this structure, to Lua addons:

```cpp
struct ImGuiSizeConstraintCallbackData
{
    ImVec2 Pos;         // The current window position, for reference. (Read Only)
    ImVec2 CurrentSize; // The current window size, for reference. (Read Only)
    ImVec2 DesiredSize; // The desired contraint to apply to the resizing of the window. (Based on the mouse position.)
};
```

You should edit the DesiredSize field to constrain the window to your liking. This value takes an ImVec2 of two floats, for example:
```lua
DesiredSize = ImVec(200, 200);
```

### Example

The following example would apply a sizing constraint to keep the window in a square shape. (Similar to aspect ratio resizing.)

```lua
function SquareResizeConstraint(data)
    data.DesiredSize = ImVec2(math.max(data.DesiredSize.x, data.DesiredSize.y), math.max(data.DesiredSize.x, data.DesiredSize.y));    
end
 
imgui.SetNextWindowSizeConstraints(0, 0, float_max, float_max, 'SquareResizeConstraint');
```

---

## ImGuiTextEditCallbackData

The ImGuiTextEditCallbackData structure contains information used for an InputText callback function. This can be useful for determining the type of callback that was fired as well as what data was used to cause the callback. 

The following data is exposed in this structure, to Lua addons:

```cpp
struct ImGuiTextEditCallbackData
{
    ImGuiInputTextFlags EventFlags;    // ImGuiInputTextFlags_Callback... value from the ImGuiInputTextFlags_ enumeration. (Read Only)
    ImGuiInputTextFlags Flags;         // The flags of the input creation call. (Read Only)
    bool                ReadOnly;      // The readonly flag of the input box. (Read Only)
    ImWchar             EventChar;     // The character that was input.
    ImGuiKey            EventKey;      // The key pressed to cause this event. (Read Only)
    char*               Buf;           // The current buffer of text in the input.
    int                 BufTextLen;    // The current length of text in buf.
    int                 BufSize;       // Maximum length that buf can hold. (Read Only)
    bool                BufDirty;      // Must be set to true if Buf or BufTextLen is modified.
    int                 CursorPos;     // The current carrot position within the input text.
    int                 SelectionStart;// The selection start position.
    int                 SelectionEnd;  // The selection end position.
     
    void DeleteChars(int pos, int count);
    void InsertChars(int pos, const char* new_text);
    bool HasSelection();
};
```

Some fields are read-only and cannot be edited.

If you edit the 'Buf' field, you must update the BufTextLen to the new length as well as set BufDirty to true in order for it to be properly updated. To do this easily you can make use of the DeleteChars and InsertChars functions which will handle the property adjustments for you.

You may also want to set CursorPos to the end of the string for a more expected result.

---

## ImGui IO Table

The ImGui IO table holds various I/O related properties and information about the current state of ImGui.

You can access this table via:

```lua
-- Includes the various defintions and such for ImGui, also adding the imgui global..
require 'imguidef';

-- Obtain the io table..
local io = imgui.io;
```

**Please Note:** The imgui.io table differs from the main imgui functions! Please be sure to read the following notes carefully!!
{: .notice--warning}

The imgui.io table differs from the functions found within the 'imgui' table. The io table is implemented in a different manner and can make use of certain types such as ImVec2, ImVec4, etc. Because of this, things are used a little differently. But it should be straight forward enough.

Here are some examples of how you can make use of the imgui.io table properties:

```lua
-- Getting the display size.. (ImVec2)
local display_x = imgui.io.DisplaySize.x;
local display_y = imgui.io.DisplaySize.y;
 
-- Setting the display size.. (ImVec2)
imgui.io.DisplaySize = ImVec2(100, 100);
 
-- Obtaining if the left mouse button is down..
local isMouseDown = imgui.io.MouseDown[0];
 
-- Setting if the left mouse button is down manually..
local mouseDown = imgui.io.MouseDown;
mouseDown[0] = true;
imgui.io.MouseDown = mouseDown;
```

Any property that is within an array must be done in the above manner. You cannot directly index these arrays and set their values. 
You must pull the array, edit it, then reset the full array to make changes.

---

## ImGui IO Table Properties

The table holds the following properties:

  * ImVec2 DisplaySize - _The current display size for ImGui to render within._
  * float DeltaTime - _Time elapsed since the last frame._
  * float IniSavingRate - _Maximum time between saving current window positions._
  * const char* IniFilename - _The path to the imgui.ini file._
  * const char* LogFilename - _The path to the imgui_log.txt file._
  * float MouseDoubleClickTime - _Time for a double-click to register._
  * float MouseDoubleClickMaxDist - _Distance threshold to stay in to validate a double-click (in pixels)._
  * float MouseDragThreshold - _Distance threshold to before considering we are dragging._
  * int KeyMap[19] - _Map of indices into the KeysDown entries array. (Used to translate key codes.)_
  * float KeyRepeatDelay - _Time before a key begins repeating while being held down._
  * float KeyRepeatRate - _Time between each key repeat while being held down._
  * void* UserData - _Custom defined user data._
  * ImFontAtlas* Fonts - _Current atlas of loaded fonts. (Not implemented for Lua usage.)_
  * float FontGlobalScale - _Global scale for all fonts to use._
  * bool FontAllowUserScaling - _Allows users to scroll in and out of ImGui when enabled._
  * ImVec2 DisplayFramebufferScale - _Used for retina displays where window coords differ from frame buffer coords._
  * ImVec2 DisplayVisibleMin - _Not used._
  * ImVec2 DisplayVisibleMax - _Not used._
  * bool WordMovementUsesAltKey - _Not used._
  * bool ShortcutsUseSuperKey - _Not used._
  * bool DoubleClickSelectsWord - _Not used._
  * bool MultiSelectUsesSuperKey - _Not used._
  * ImVec2 MousePos - _The current position of the mouse._
  * bool MouseDown[5] - _Current mouse button states. (Starts at index 0: left, right, middle, +extras)_
  * float MouseWheel - _Current mouse wheel rotation offset._
  * bool MouseDrawCursor - _Enables ImGui to render a cursor._
  * bool KeyCtrl - _Flag that is true if Ctrl is pressed._
  * bool KeyShift - _Flag that is true if Shift is pressed._
  * bool KeyAlt - _Flag that is true if Alt is pressed._
  * bool KeySuper - _Flag that is true if Windows key is pressed._
  * bool KeysDown[512] - _Array of flags set to true if various keys are down._
  * ImWchar InputCharacters[16 + 1] - _List of characters currently being input._
  * bool WantCaptureMouse - _Flag that is true if ImGui is currently capturing the mouse._
  * bool WantCaptureKeyboard - _Flag that is true if ImGui is currently capturing the keyboard._
  * bool WantTextInput - _Flag that is true if ImGui is currently capturing input._
  * float Framerate - _Estimated frames per second._
  * int MetricsAllocs - _Number of current memory allocations._
  * int MetricsRenderVertices - _Number of current vertices being rendered._
  * int MetricsRenderIndices - _Number of indices being rendered._
  * int MetricsActiveWindows - _Number of windows that are currently active._
  * ImVec2 MousePosPrev - _The previous mouse position during the last frame._
  * ImVec2 MouseDelta - _The current mouse delta._
  * bool MouseClicked[5] - _Array of flags that determine if a mouse button was clicked since the last frame._
  * ImVec2 MouseClickedPos[5] - _Array of positions that hold where a given button clicked since the last frame._
  * float MouseClickedTime[5] - _Array of times that hold when a given button was clicked since the last frame._
  * bool MouseDoubleClicked[5] - _Array of flags that hold if a mouse button was double clicked since the last frame._
  * bool MouseReleased[5] - _Array of flags that hold if a mouse button was released since the last frame._
  * bool MouseDownOwned[5] - _Array of flags that hold if a click started within an ImGui controls space since the last frame._
  * float MouseDownDuration[5] - _Array of time that holds the duration since a mouse button was clicked down._
  * float MouseDownDurationPrev[5] - _Array of time that holds the duration since a mouse button was clicked down (previously)._
  * float MouseDragMaxDistanceSqr[5] - _Array of distance (square rooted) that the mouse has traveled since a mouse click._
  * float KeysDownDuration[512] - _Array of time that holds the duration of a key down._
  * float KeysDownDurationPrev[512] - _Array of time that holds the duration of a key down (previously)._

---

## ImGui Style Table

The ImGui Style table the current visual style of ImGui and the various properties that can alter it.

You can access this table via:

```lua
-- Includes the various defintions and such for ImGui, also adding the imgui global..
require 'imguidef';

-- Obtain the style table..
local style = imgui.style;
```

**Please Note:** The imgui.style table differs from the main imgui functions! Please be sure to read the following notes carefully!!
{: .notice--warning}

The imgui.style table differs from the functions found within the 'imgui' table. The style table is implemented in a different manner and can make use of certain types such as ImVec2, ImVec4, etc. Because of this, things are used a little differently. But it should be straight forward enough.

Here are some examples of how you can make use of the imgui.style table properties:

```lua
-- Obtain the style table..
local s = imgui.style;
 
-- Set the rounding properties to 0..
s.GrabRounding = 0;
s.FrameRounding = 0;
s.ScrollbarRounding = 0;
s.WindowRounding = 0;
 
-- Set a color to black..
local colors = imgui.style.Colors;
colors[ImGuiCol_WindowBg] = ImVec4(0.0, 0.0, 0.0, 1.0);
imgui.style.Colors = colors;
```

Any property that is within an array must be done in the above manner. You cannot directly index these arrays and set their values. 
You must pull the array, edit it, then reset the full array to make changes.

---

## ImGui Style Table Properties

The table holds the following properties:

  * float Alpha - _Global alpha amount that applies to the entire ImGui rendering._
  * ImVec2 WindowPadding - _The default window padding applied to windows._
  * ImVec2 WindowMinSize - _The minimum window size._
  * float WindowRounding - _The amount of rounding to apply to the window corners._
  * ImVec2 WindowTitleAlign - _The alignment of the title of a window._
  * float ChildWindowRounding - _Child window corner rounding._
  * ImVec2 FramePadding - _Padding applied to framed rectangles._
  * float FrameRounding - _Rounding applied to framed rectangles._
  * ImVec2 ItemSpacing - _The amount of spacing between widgets and lines._
  * ImVec2 ItemInnerSpacing - _The amount of spacing within elements of a composed widget. (ex. label inside of a slider.)_
  * ImVec2 TouchExtraPadding - _Padding added to controls to enhance touch usage. (Not used.)_
  * float IndentSpacing - _Default horizontal indentation amount._
  * float ColumnsMinSpacing - _Minimum horizontal spacing between two columns._
  * float ScrollbarSize - _Default size of a scroll bar. (Width if vertical, Height if horizontal.)_
  * float ScrollbarRounding - _The amount of rounding to apply to scrollbar corners._
  * float GrabMinSize - _Minimum width/height of a grab box for sliders / scrollbars._
  * float GrabRounding - _The amount of rounding to apply to grips._
  * ImVec2 DisplayWindowPadding - _Window positions are clamped to be visible within the display area by at least this amount. Only covers regular windows._
  * ImVec2 DisplaySafeAreaPadding - _If you cannot see the edge of your screen (e.g. on a TV) increase the safe area padding. Covers popups/tooltips as well regular windows._
  * bool AntiAliasedLines - _Enable anti-aliasing on lines / borders._
  * bool AntiAliasedShapes - _Enable anti-aliasing on filled shapes._
  * float CurveTessellationTol - _Tessellation tolerance. Decrease for highly tessellated curves (higher quality, more polygons), increase to reduce quality._
  * ImVec4 Colors[43] - _Array of colors used by ImGui to render the theme. (See the list of ImGuiCol\_ properties in the imgui.lua library file for more info.)_