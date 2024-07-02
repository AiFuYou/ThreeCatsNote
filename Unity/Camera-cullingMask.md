在 Unity 中，Camera 对象的 `cullingMask` 属性用于决定哪个层次（Layer）的物体会被渲染。`cullingMask` 实际上是一个位掩码（bitmask），每一位对应一个层次（Layer）。当你设置 `cullingMask` 时，可以选择要渲染的层次。

你可以在编辑器的 Camera 组件中设置 `cullingMask`，也可以通过脚本进行设置。

### 使用编辑器设置 `cullingMask`

1. 在 Hierarchy 视图中选中你的 Camera 对象。
2. 在 Inspector 视图中找到 Camera 组件。
3. 找到 `Culling Mask` 选项，点击这个选项会显示层次列表，其中每个层次前面有复选框，你可以选择需要被渲染的层次。

### 使用脚本设置 `cullingMask`

在脚本中设置 `cullingMask` 可以使用位运算符或者直接使用整数值。

#### 示例代码：

```csharp
using UnityEngine;

public class CameraCullingMaskExample : MonoBehaviour
{
    public Camera camera;

    void Start()
    {
        // 假设你已经在编辑器中将 Camera 关联到该变量
        if (camera == null)
        {
            camera = GetComponent<Camera>();
        }

        // 设置仅渲染默认层次 (Default Layer)
        camera.cullingMask = 1 << LayerMask.NameToLayer("Default");

        // 设置不渲染任何东西
        // camera.cullingMask = 0;

        // 设置渲染所有层次
        // camera.cullingMask = ~0;

        // 设置渲染多个层次，比如默认层次 (Default) 和透明物体层次 (TransparentFX)
        camera.cullingMask = (1 << LayerMask.NameToLayer("Default")) | 
                             (1 << LayerMask.NameToLayer("TransparentFX"));
    }
}
```

#### 说明：

1. **单层掩码**：
   使用 `1 << LayerMask.NameToLayer("LayerName")` 设置一个特定层次的掩码。例如：
   ```csharp
   camera.cullingMask = 1 << LayerMask.NameToLayer("Default");
   ```
   这将设置 Camera 只渲染 "Default" 层次。

2. **多层掩码**：
   使用按位或运算符 (`|`) 组合多个层次的掩码。例如：
   ```csharp
   camera.cullingMask = (1 << LayerMask.NameToLayer("Default")) | 
                        (1 << LayerMask.NameToLayer("TransparentFX"));
   ```
   这将设置 Camera 渲染 "Default" 和 "TransparentFX" 两个层次。

3. **全部层次**：
   设置 Camera 渲染所有层次：
   ```csharp
   camera.cullingMask = ~0;
   ```

4. **不渲染任何层次**：
   设置 Camera 不渲染任何层次：
   ```csharp
   camera.cullingMask = 0;
   ```

### 常见层次（层）：

默认情况下，Unity 提供了一些内置的层次列表，包括：

- Default
- TransparentFX
- Ignore Raycast
- Water
- UI

你也可以在编辑器中自定义层次。在 Unity 编辑器菜单中的 `Edit -> Project Settings -> Tags and Layers` 中可以添加和管理自定义层次。

通过正确设置 `cullingMask`，你可以控制 Camera 所渲染的对象，这在性能优化和特效实现中非常有用。
