# Ready For Nanite

<img width="1280" height="640" alt="Preview" src="https://github.com/user-attachments/assets/afce9abe-8c75-4e14-a13f-9b8156cff29b" />



Wiki: https://github.com/WanderFox/Ready_For_Nanite_P/wiki

Blenderkit: https://www.blendkit.com/asset-gallery-detail/c961d8c3-eaf9-4774-b2a3-c27f55df8202/?query=author_id%3A1620852

Gumroad: https://fly4xy.gumroad.com/l/ready-for-nanite


**Languages:** [English](#english) · [Русский](#russian) · [中文](#chinese)

---

<a name="english"></a>
<details open>
<summary><b>🇬🇧 English</b></summary>

<br>

# Ready For Nanite

A Blender addon that turns meshes with alpha-channel cutouts (foliage, grass, bushes, cloth, grates, etc.) into geometry ready for Nanite in Unreal Engine.

Usually such objects are just a plane or a simple shape with a texture where transparent areas are simply cut out by an alpha mask. Nanite can't work with that — it needs real geometry. The addon reads the alpha channel of the texture, finds the borders of opaque areas and transparent holes, and builds real 3D geometry from them with proper UVs and normals.

## What the addon can do

- Automatically detects where the texture has transparency and builds the object's contour from it.
- Handles holes inside the object separately (for example, gaps between leaves).
- Preserves the UV layout and normals of the original model on the new geometry.
- Works with multiple materials and with objects made of many separate pieces.
- Supports caching: if you have many identical bushes or leaves, the addon won't recompute the same thing over and over — this greatly speeds up work on large scenes.
- Can estimate the approximate processing time before starting.
- Has a quick test mode — processes only one instance of each unique piece so you can preview the result without waiting for the full pass.
- Problem objects (no UVs, no texture, etc.) are not lost — they are placed into a separate collection marked `_broken`.
- Source objects can be kept, hidden, or deleted — your choice.

## Interface parameters

**Alpha Threshold** — transparency threshold. Anything brighter than this value is considered body, anything darker is background or a hole. Lower value — captures more semi-transparent edges, higher — cuts more aggressively.

**Contour Classification Threshold** — the threshold the addon uses to decide whether a contour is body or a hole. If the fraction of opaque pixels inside a contour is greater than this value — it's body, if less — it's a hole. Lower it if holes containing geometry are being misclassified as body.

**Min Island Area** — minimum area of a piece of the resulting geometry. Anything smaller is deleted. Helps remove small debris. Zero — nothing is deleted.

**Simplify Tolerance (Areas)** — how much the body contours can be simplified. Higher value — fewer points, faster and coarser. Lower — more accurate shape, more vertices.

**Min Contour Area UV (Areas)** — minimum contour area for body. Anything smaller is discarded before geometry is built.

**Simplify Tolerance (Holes)** — same as Simplify Tolerance (Areas) but for holes. Lets you keep the body coarse while holes stay detailed.

**Min Contour Area UV (Holes)** — same as Min Contour Area UV (Areas) but for holes.

**Sync holes to areas** (button) — copies the area settings into the hole settings with one click.

**Max Texture Rect** — maximum size of the texture rectangle taken into processing. If the UV layout is larger, the texture is downsampled. Speeds up work on large textures but reduces contour accuracy.

**Hole Thickness** — thickness applied to flat hole contours before the boolean operation. Needed so hole cutting works correctly. If the model is small, the value may be too large — then holes end up bigger than they should be.

**Target Density** — triangle density per square unit of scene area. The source mesh is densified up to this density before transferring UVs and normals. Higher — more accurate transfer and finer detail, but slower.

**UV Map** — which UV layout is used. Auto picks the first available one.

**Evolutionary Optimization** — enables caching for repeated UV layouts and shapes. On large scenes with repeating objects it speeds up work several times over.

**Reuse Equivalent Source Mesh** — enables caching for identical source meshes. Only works together with Evolutionary Optimization.

**Delete Source Objects** — delete source objects after processing.

**Hide Source Objects** — hide source objects after processing.

**Estimate Processing** (button) — estimates approximate processing time for the selected objects.

**Reset to Defaults** (button) — resets all settings to their default values.

**Quick Test** (button) — processes only one instance of each unique piece. Lets you preview the result quickly.

**Process Selected** (button) — the main run, processes the selected objects.

## License

GNU General Public License v3.0 or later.

</details>

---

<a name="russian"></a>
<details>
<summary><b>🇷🇺 Русский</b></summary>

<br>

# Ready For Nanite

Плагин для Blender, который превращает меши с вырезами по альфа-каналу (листва, трава, кусты, ткани, решётки и т.п.) в геометрию, готовую для Nanite в Unreal Engine.

Обычно такие объекты — это плоскость или простая форма с текстурой, где прозрачные участки просто отсекаются альфа-маской. Для Nanite это не подходит: он не умеет работать с альфа-маской, ему нужна настоящая геометрия. Плагин читает альфа-канал текстуры, находит границы непрозрачных участков и прозрачных дырок, и строит по ним реальную 3D-геометрию с правильными UV и нормалями.

## Что умеет плагин

- Автоматически определяет, где на текстуре есть прозрачность, и строит по ней контур объекта.
- Отдельно обрабатывает дырки внутри объекта (например, просветы между листьями).
- Сохраняет UV-развёртку и нормали исходной модели на новой геометрии.
- Работает с несколькими материалами и с объектами, состоящими из множества отдельных кусков.
- Поддерживает кэширование: если у вас много одинаковых кустов или листьев, плагин не будет пересчитывать одно и то же заново — это сильно ускоряет работу на больших сценах.
- Умеет оценивать примерное время обработки до её запуска.
- Есть режим быстрого теста — обрабатывает только один экземпляр каждого уникального куска, чтобы можно было посмотреть результат, не дожидаясь полного прохода.
- Проблемные объекты (без UV, без текстуры и т.п.) не теряются — они складываются в отдельную коллекцию с пометкой `_broken`.
- Исходные объекты можно оставить, скрыть или удалить — на выбор.

## Параметры интерфейса

**Alpha Threshold** — порог прозрачности. Всё, что светлее этого значения, считается телом, всё, что темнее — фоном или дыркой. Меньше значение — захватывает больше полупрозрачных краёв, больше — режет агрессивнее.

**Contour Classification Threshold** — порог, по которому плагин решает, что перед ним: тело или дырка. Если внутри контура непрозрачных пикселей больше этого значения — это тело, если меньше — дырка. Понизьте, если дырки с геометрией внутри ошибочно определяются как тело.

**Min Island Area** — минимальная площадь куска готовой геометрии. Всё, что меньше, удаляется. Помогает убрать мелкий мусор. Ноль — ничего не удаляется.

**Simplify Tolerance (Areas)** — насколько сильно можно упрощать контуры тела. Больше значение — меньше точек, быстрее и грубее. Меньше — точнее форма, больше вершин.

**Min Contour Area UV (Areas)** — минимальная площадь контура тела. Всё, что меньше, отбрасывается ещё до построения геометрии.

**Simplify Tolerance (Holes)** — то же самое, что Simplify Tolerance (Areas), но для дырок. Можно держать тело грубым, а дырки — детальными.

**Min Contour Area UV (Holes)** — то же самое, что Min Contour Area UV (Areas), но для дырок.

**Sync holes to areas** (кнопка) — копирует настройки областей в настройки дырок одним нажатием.

**Max Texture Rect** — максимальный размер прямоугольника текстуры, который берётся в обработку. Если UV-развёртка больше, текстура уменьшается. Ускоряет работу на больших текстурах, но снижает точность контуров.

**Hole Thickness** — толщина, которая придаётся плоским контурам дырок перед булевой операцией. Нужна, чтобы вырезание дырок работало корректно. Если модель мелкая, значение может оказаться слишком большим — тогда дырки получатся больше, чем должны.

**Target Density** — плотность треугольников на квадратную единицу сцены. Исходный меш уплотняется до этой плотности перед переносом UV и нормалей. Чем выше — тем точнее перенос и мельче детали, но медленнее.

**UV Map** — какая UV-развёртка используется. Auto берёт первую доступную.

**Evolutionary Optimization** — включает кэш для повторяющихся UV-развёрток и форм. На больших сценах с повторяющимися объектами ускоряет работу в разы.

**Reuse Equivalent Source Mesh** — включает кэш для одинаковых исходных мешей. Работает только вместе с Evolutionary Optimization.

**Delete Source Objects** — удалить исходные объекты после обработки.

**Hide Source Objects** — скрыть исходные объекты после обработки.

**Estimate Processing** (кнопка) — оценивает примерное время обработки для выделенных объектов.

**Reset to Defaults** (кнопка) — сброс всех настроек к значениям по умолчанию.

**Quick Test** (кнопка) — обрабатывает только один экземпляр каждого уникального куска. Позволяет быстро посмотреть результат.

**Process Selected** (кнопка) — основной запуск обработки выделенных объектов.

## Лицензия

GNU General Public License v3.0 или новее.

</details>

---

<a name="chinese"></a>
<details>
<summary><b>🇨🇳 中文</b></summary>

<br>

# Ready For Nanite

一个 Blender 插件，可以把带 alpha 通道镂空的网格（树叶、草、灌木、布料、栅栏等）转换成适用于 Unreal Engine 中 Nanite 的几何体。

通常这类物体只是一个平面或简单形状，配上纹理，透明部分由 alpha 遮罩直接裁掉。Nanite 无法处理这种方式——它需要真实几何体。本插件会读取纹理的 alpha 通道，找到不透明区域的边界和透明孔洞，并据此构建带有正确 UV 和法线的真实 3D 几何体。

## 插件功能

- 自动检测纹理中哪里有透明区域，并据此构建物体轮廓。
- 单独处理物体内部的孔洞（例如树叶之间的缝隙）。
- 在新几何体上保留原模型的 UV 展开和法线。
- 支持多材质，以及由许多独立碎片组成的物体。
- 支持缓存：如果你有很多相同的灌木或树叶，插件不会反复计算相同的内容——在大场景中这能大幅提速。
- 可以在开始处理前估算大致处理时间。
- 有快速测试模式——只处理每个唯一碎片的一个实例，让你无需等待完整流程就能预览结果。
- 有问题的物体（没有 UV、没有纹理等）不会丢失——它们会被放进一个标有 `_broken` 的独立集合。
- 源物体可以保留、隐藏或删除——由你选择。

## 界面参数

**Alpha Threshold** — 透明度阈值。比这个值更亮的都算作实体，更暗的都算作背景或孔洞。值越小——保留更多半透明边缘，值越大——裁剪越激进。

**Contour Classification Threshold** — 插件用来判断某个轮廓是实体还是孔洞的阈值。如果轮廓内不透明像素的比例大于这个值——就是实体，小于——就是孔洞。如果带几何体的孔洞被误判为实体，就调低这个值。

**Min Island Area** — 生成几何体中单个碎片的最小面积。比这个值更小的都会被删除。用于清理小碎屑。零——不删除任何东西。

**Simplify Tolerance (Areas)** — 实体轮廓可以被简化到什么程度。值越大——点越少，更快但更粗糙。值越小——形状更精确，顶点更多。

**Min Contour Area UV (Areas)** — 实体的最小轮廓面积。比这个值更小的会在构建几何体之前就被丢弃。

**Simplify Tolerance (Holes)** — 与 Simplify Tolerance (Areas) 相同，但作用于孔洞。可以保持实体粗糙，而孔洞保持精细。

**Min Contour Area UV (Holes)** — 与 Min Contour Area UV (Areas) 相同，但作用于孔洞。

**Sync holes to areas**（按钮）— 一键把区域设置复制到孔洞设置。

**Max Texture Rect** — 参与处理的纹理矩形的最大尺寸。如果 UV 展开更大，纹理会降采样。在大纹理上能加速，但会降低轮廓精度。

**Hole Thickness** — 在布尔运算之前给平面孔洞轮廓赋予的厚度。这是为了让孔洞切割正常工作。如果模型很小，这个值可能太大——那样孔洞会比应有的更大。

**Target Density** — 每平方场景单位的三角形密度。在传递 UV 和法线之前，源网格会被加密到这个密度。值越高——传递越精确，细节越细，但越慢。

**UV Map** — 使用哪个 UV 展开。Auto 会选择第一个可用的。

**Evolutionary Optimization** — 为重复的 UV 展开和形状启用缓存。在有大量重复物体的大场景中可以把速度提高好几倍。

**Reuse Equivalent Source Mesh** — 为相同的源网格启用缓存。只能与 Evolutionary Optimization 一起工作。

**Delete Source Objects** — 处理之后删除源物体。

**Hide Source Objects** — 处理之后隐藏源物体。

**Estimate Processing**（按钮）— 估算所选物体的大致处理时间。

**Reset to Defaults**（按钮）— 把所有设置恢复为默认值。

**Quick Test**（按钮）— 只处理每个唯一碎片的一个实例。让你可以快速预览结果。

**Process Selected**（按钮）— 主运行按钮，处理选中的物体。

## 许可证

GNU General Public License v3.0 或更高版本。

</details>
