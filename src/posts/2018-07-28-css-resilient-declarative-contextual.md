---
favorite: true
title: "[CSS] لغة صامدة - لغة تصريحية - لغة سياقية"
tags:
  - "css"
scope: "s-article"
lang: "ar"
thumbnail: "/assets/images/cards/css-resilient-declarative-contextual.png"
---


قضيت الكثير من الوقت أفكر فيما يمكن أن يقوم بتعريف وتكوين مفهوم واضح لـ "آلية العمل" أو "العقلية" التي تمتلكها CSS وتعمل بها. بعض الناس قد اقتربوا من "القبض" على ذلك المفهوم، والبعض الآخر لم يفعل. ويتهيأ لي أنني لو أستطعت أن أضع يدي على ذلك المقصد، لربما تصبح لغة CSS أكثر منطقية في الفهم لأولئك الذين يعانون أثناء العمل معها.

وكانت رغبتي في الإستفاضة وتوضيح بعض من تلك الأمور هي واحدة من الأشياء التي حفزتني على كتابة [CSS in Depth](https://www.manning.com/books/css-in-depth). واليوم أردت أن ألقي الضوء على ثلاث خصائص أساسية ومفتاحية تتميز بها لغة التنسيق CSS عن باقي لغات البرمجة التقليدية، وهي أنها: لغة مرنة وصامدة، لغة تصريحية، لغة سياقية. ثلاثة جوانب رئيسية من اللغة، بفهمهم؛ نصبح على مقربة من فهم متقدم ومتعمق أكثر للغة CSS ومن ثَمَّ التمكن منها واحترافها.

<div class="c-headline">Resilient</div>

## CSS لغة مرنة - صامدة
في حال أن لديك ملفًا يضم مجموعة من أكواد JavaScript، وأخترت منه جزءًا ما بشكل عشوائي، وقمت بحذف ذلك الجزء؛ فعلى الأغلب، الصفحة أو التطبيق القائم على ذلك الملف، سوف ينهار ويتوقف عن العمل، وسيؤثر ذلك على باقي الأكواد في الملف، وربما يُصبح معظمها - إن لم يكن الصفحة أو التطبيق بأكمله- عديم الفائدة وبلا عمل. حاول الآن أن تفعل الشيء نفسه في CSS؛ ربما لن تعلم حتى بأن شيئًا ما قد تغير؛ فعلى الأغلب، باقي أكواد الملف التي تبعُد عن ذلك الجزء الناقص أو الذي يحتوي على أخطاء، سوف تستمر في العمل بشكل طبيعي كما من المفترض لها أن تعمل.

نحن نسمي هذا صمود "resilience". إن لغتي HTML و CSS صُممتا خصيصًا لتمتلكا القدرة على تدارك الأخطاء الداخلية للكود وامتصاصها. في حين تواجد خطأ ما، هنا تعمل CSS بشكل ما يجعل المتصفح يتدارك الخطأ أو يتجاهل ذلك الجزء الذي يتواجد به الخطأ ثم يستكمل قراءة باقي الأكواد ويُظهر لنا نتيجة ما أخيرًا بدلًا من أن يُظهر الأخطاء مسببًا لانهيار الصفحة.

قد يبدو ذلك شيئًا غير عمليٍ من ناحية فحص الكود ([Debugging](https://en.wikipedia.org/wiki/Debugging))؛ فلو لم يُظهر المتصفح أخطاء الكود، كيف لك أن تعرف أن هناك خطأ ما وما هو مصدر ذلك الخطأ؟! لكنّ هذا جزء أساسي من آلية عمل CSS، وهو سِمة أصيلة ومنسوجة داخل نسيج وبنية اللغة نفسها. قد يأخذ ذلك بعض الوقت للإعتياد عليه ومجاراته، لكنّي أعترف لك، بمجرد أن تفهمه، تستطيع حينها أن تطمئن أثناء استخدام بعض الخواص التي لا تزال غير مدعومة في كل المتصفحات. هذا هو ما يجعل ما يسمى بـ "التحسين التدريجي" في تصميم الويب "[Progressive Enhancement](https://www.smashingmagazine.com/2009/04/progressive-enhancement-what-it-is-and-how-to-use-it/)" أمرًا ممكنًا.

> عند استخدامك لمبدأ التحسين التدريجي في تصميم الويب، يمكنك أن تعمل على تهيئة الكود الخاص بك بشكل ما يجعله يعمل دائمًا آيًا كانت الأوضاع أو السيناريوهات التي يمر خلالها.
> — [جين سيمونز](https://www.youtube.com/watch?v=u00FY9vADfQ)، عضو بـ CSS Working Group

الكود التالي هو مثال على تخطيط لجزءٍ من صفحةِ ويب باستخدام التخطيط الشبكي [CSS Grid](https://www.w3.org/TR/css-grid-1/). أنه يعمل على المتصفحات التي تفهم وتدعم CSS Grid، وبنفس الوقت يعمل على المتصفحات التي لا تفهم ولا تدعم CSS Grid. سوف يكون مختلفًا وغير مكتملًا بشكل طفيف في تلك المتصفحات التي لا تدعم CSS Grid (الأحجام والمقاسات الخاصة بالعناصر ستختلف قليلًا)، لكن في النهاية سوف يظل لدينا تخطيطًا للصفحة "Layout" بنفس الشكل تقريبًا :

``` css
.portfolio {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
}

.portfolio__item {
  display: inline-block;
  max-width: 600px;
}
```

في حالة أن كان هناك متصفحًا لا يفهم التعريفات الخاصة بنظام التخطيط الشبكي CSS Grid فإنه سوف يتجاهلها، مستمرًا في طريقه تجاه الأكواد الثانوية البديلة، لأنها هي من سيقوم بالعمل في ذلك الوضع. بينما لو كان متصفحًا يفهم CSS Grid ويدعمه فإنه سوف يقرأ تعريفات CSS Grid ويستخدمها، ويتجاهل التعريف `display: inline-block`، (لأن ذلك هو ما صمم من أجله النظام الشبكي CSS Grid). [جين سيمونز](https://www.youtube.com/watch?v=u00FY9vADfQ) أطلقت على ذلك - بمزاح يتضمن الجدية- ما يسمى "CSS الكـم" أو "Quantum CSS". فبإمكانك أن تأخذ خاصية من خواص CSS و "تستخدمها ولا تستخدمها في الوقت نفسه. وستكون تلك الخاصية تعمل ولا تعمل في الوقت نفسه."

هذا المفهوم لسلوك "الإحتياطية" أو "الإحتمالية" - أي العمل في ظل ظروف وسيناريوهات مختلفة وأخذ وضع الإستعداد الدائم - هو جزء لا يتجزأ من استخدام لغة CSS، وهو أمرٌ غير مألوف بالنسبة لمعظم لغات البرمجة التقليدية.



<div class="c-headline">Declarative</div>

## CSS لغة تصريحية - تعريفية
في لغة Javascript، أنت تعطي التعليمات خطوة بخطوة لكي تجعل شيئًا ما يحدث. أما في CSS فأنت تخبر المتصفح ما الذي تريده أن يحدث، وهو يتولي مهمة و كيفية حدوث ذلك. هذا ضروري جدًا لأِن تأخذه بعين الإعتبار وتفهمه جيدًا، فإن فهمته؛ فإن CSS ستقوم بكل العمل الشاق من أجلك! وإن لم تفهمه؛ فسوف تجد نفسك تسبح ضد التيار الطبيعي للغة وتصاب بالإحباط عند كل منعطف.

بشكل واضح، الكتابة في CSS هي إنشاء نظام من التصريحات أو التكليفات. أنت لا تخبر المتصفح أين تريد أن تضع كل عنصر من عناصر الصفحة؛ أنت تخبره كم المسافة التي تريد وضعها بين العناصر، ثم تدعه هو يأخذ كل عنصر ويضعه حيث مكانه الذي ينتمي إليه في الصفحة بناءًا على ما كُتب من تعريفات (Declarations). أنت لا تخبره - أو لا ينبغي عليك أن تخبره أصلًا - كم الطول المناسب لكي يصنع حاوية (container)؛ أنت تدعه يكتشف ذلك وقت المعالجة (Rendering) عندما يرى ويتعرف على المحتويات الداخلية للـ(container) حيث تكون التعريفات والتنسيقات الخاصة بها قد طُبقت في الصفحة، وكمْ من العرض متوفرًا في صفحة المتصفح أو ما يعرف بإطار العرض (viewport).

هناك العديد من المتغيرات والإعتبارات التي يتعين مراعاتها وأخذها في الحسبان، والهدف الأساسي في CSS هو الإهتمام بذلك بدلًا عنك فتصبِح غير مضطرًا للقلق بشأنهم. فقط قم بتعريف بعض التكليفات، ودع اللغة تهتم بإخراج التفاصيل.

{% Note {
  text: "<h5>■ ما معنى أن CSS لغة تصريحية (Declarative Language)؟</h5>CSS باعتبارها لغة تصريحية فهي تسمح لك أن تَوصِف أو تُصرّح أو تعرّف للمتصفح ماذا تريد أن يحدث أو ما الذي لا تريده أن يحدث، والمتصفح هو من يتولي الكيفية أو الطريقة في تنفيذ المطلوب وإخراجه. في كلمات أقل: (التركيز على وصف ما نريد تنفيذه وليس التركيز على كيفية تنفيذه). وذلك من أجل توفير سهولة وسلاسة في كتابة الأكواد وإزالة القلق بشأن كل التعقيدات والأمور المرهقة الأخرى التي تحدث من وراء الكواليس أثناء عمليات المعالجة."
} %}

#### مثال بسيط
دعنا ننظر لهذا التعريف لدقيقة من الزمن `font-size: 2em` ما الذي يقوم بفعله؟ من المفترض أنه يزيد من حجم الخط. لكنّ هذا ليس كل شيء. أنه أيضًا سيقوم باعادة تهيئة التفاف النص حول الأسطر داخل مساحة العرض المحدد للـ(container) ليتلائم ويتناسب مع حجم الخط الذي قمنا بتعريفه للتو، في كلمات أقل: سيجعل النص بالحجم الجديد متلائمًا ومتسقًا مع كل سطر. وهذا بدوره، في الغالب، سيزيد من عدد الأسطر للنص، وأيضًا سيعمل على زيادة ارتفاع الـ(container) لِيضُم الأسطر الجديدة الزائدة، وبناءًا على زيادة ارتفاع الـ(container)، فإن كل شيء يوجد أسفله سوف يتحرك للأسفل تِباعًا. وأخيرًا، سيقوم أيضًا بتخصيص قيمة جديدة للدلالة المحلية لوحدة القياس `em`، وبالتالي فإن أي خواص أخرى داخل هذا العنصر تستخدم الوحدة `em` في تعريف قياساتها، سوف تقوم بتحديث قيمها المقدرة لتتطابق مع التخصيص الجديد لقيمة الخط المحلّي المعرّف باستخدام الوحدة `em`.

هذا تعريف واحد وقد أنشأ مجموعة كبيرة -وبالجملة- من التغيرات في صفحة الويب. وجميعها تكون بالضبط كما ينبغي لها؛ فالمحتوى سيقوم بتهيئة نفسه دائمًا ليتلائم مع المساحة، والعناصر لن ينتهي بها الحال متداخلة مع بعضها البعض بشكل شاذ، وأي تعريفات جديدة يتم تعريفها وتكون مرتبطة ومتعلقة بحجم الخط ( مثل الهوامش الداخلية Padding أو خواص أخرى) سوف تتغير تباعًا لتتطابق مع التخصيص الجديد لقيمة حجم الخط. كل هذه التفاصيل ليس عليك أن تقلق حيالها، فالمتصفح هو من يقوم بكل الحسابات والعمليات ثم يـُتِم العمل بشكل افتراضي (by default).

بإمكانك أيضًا منع تلك التغيرات من الحدوث. فيمكن أن تضع حدًا أقصى لارتفاع الـ(container) باستخدام التعريفات `max-height` و `overflow: hidden`، وأيضًا يمكن إعادة تعريف القيم الخاصة بالهوامش الداخلية (padding) باستخدام وحدات قياس أخرى بدلًا من `em` مثل `rem` أو `px` حتى لا تكون تابعة لحجم الخط المحلّي المعرّف باستخدام الوحدة `em`. هذه الميزات هي جزء مثير للإهتمام في CSS؛ فأحيانا أنت لا تخبر المتصفح ماذا عليه أن يفعل، وإنما تخبره وبشكل واضح ما ليس عليه أن يفعله.

#### المعروف الذي قدمته لنا أنظمة التخطيط في CSS
هناك بعض من الخصائص والتقنيات الجديدة في CSS والتي تفعل وتقدم أكثر بكثير مما سبق ذكره، يقع على مقدمتهم نظامي Flexbox و CSS Grid. بعدد قليل من التعريفات التي تقدمها للمتصفح؛ يُصبح باستطاعتك أن تنشيء تخطيط شبكي (Grid Layout) مرن جدًا و "يعمل" بلا مقدمات. وليس عليك القلق حيال الأوضاع والحالات المحيطة لتلك المهمة؛ فأنت فقط تخبر المتصفح وتقول: "ضع هذه القوالب (boxes) في مجموعة من الأعمدة (columns) ذات عرض `400px`"، وسوف يحدث ذلك مكلفًا إياك كتابة ما يقرب من ثلاثة أسطر فقط من الكود!

لو أنك أقدمت على فعل ذلك بشكل إلزامي وتفصيلي، فستكون بحاجة إلى التعامل مع الكثير من الحالات والسيناريوهات المختلفة للمحتوي التي من المحتمل حدوثها. مثل: ماذا لو كانت هناك كلمة طويلة جدًا داخل قالب من تلك القوالب؟ ماذا لو أن صفحة المتصفح أو إطار العرض (viewport) كان صغيرًا جدًا كشاشة جهاز لوحي مثًلا؟ وماذا لو كان كبيرًا جدًا كشاشات ذات حجم أكبر من المعتاد؟! ماذا لو ان أحد تلك القوالب كان ممتلئًا بالكثير من المحتوى وآخر لا يملك سوى كلمات قليلة فقط؟ ولكن في CSS، أنت لست بحاجة للتفكير في كل تلك الأمور. كل العمل الشاق قد تم تهيئته مسبقًا في خصائص ومواصفات اللغة (CSS Specifications) والمتصفح هو من يعتني بذلك ويتواصل معه من أجل أن ينفذ لك ما تريد. وهذا يبين مدى قوة CSS كونها لغة تصريحية (Declarative Language).

ولكنّ هذا كان يأتي مع نوعًا من التنازل؛ فلو أن تلك "اللغة التصريحية" لا يمكنها دعم أو تحقيق شيء ما مخصص تريده (على سبيل المثال، Masonry Layout )، ستجد نفسك مضطرًا إلى استخدام أحد الهاكات (Hacks) المستفزة، أو اللجوء لـ JavaScript لمساعدتك في تحقيق مُرادك. ولسنوات كان ذلك جزءًا هامًا وكبيرًا في تطوير لغة CSS، وبكل امتنان، ومع ظهور نظامي Flexbox و CSS Grid، أصبح بإمكاننا أن نفعل أكثر مما كنا نستطيع فعله في الماضي، بدون أي هاكات (ونعم، الـfloats كانت Hack). أخيرًا، لو أن نواحي القصور تلك لا زالت تعكر عليك صفوك، أقترح عليك بالقراءة عن [CSS Houdini](https://www.smashingmagazine.com/2016/03/houdini-maybe-the-most-exciting-development-in-css-youve-never-heard-of/), والتي بدأت في شق طريقها للعمل على المتصفحات.

<div class="c-headline">Contextual</div>

## CSS لغة سياقية
مع بزوغ عصر الـ React.js، أصبحنا نهتم ونمشي على خُطى "الإتجاه" بالغ الفائدة والأهمية في التطوير وهو التطوير القائم على المكونات - التطوير التركيبي (Modular, Component-based Development) . في CSS يمكن أيضًا أن نفعل ذلك بإتقان، باستخدام منهجيات مثل "BEM" و "SMACSS" و "CSS-in-JS". وأنا لا أريد التقليل هنا من شأن ذلك، لأن هذا أسلوب تفكير هام وضروري أثناء العمل على مشاريع كبيرة وضخمة. لكنّي أعتقد أنه وبنفس القدر من الأهمية، علينا الإقرار بأن CSS ليست موديولية "Modular" بنسبة 100%، وليس عليها أن تكون كذلك.

هناك سببين لذلك. السبب الأول، والأكثر وضوحًا، وهو أن التطبيق الذي لديك ينبغي أن يحصل على بعض التنسيقات العمومية (global styles)؛ فعلى الأغلب ستحتاج إلى إلى تخصيص خط من الخطوط، وكذلك تخصيص حجم لذلك الخط على مستوى الصفحة بأكملها. وهذه القيم (values) التي قمت بتخصيصها، سوف توّرَث بعد ذلك لكل العناصر المتفرعة داخل الصفحة ما لم يطغي على أحدها قيم وتخصيصات أخرى جديدة أنت قمت بها، في نوع الخط وحجمه على سبيل المثال. وأيضًا ربما سترغب بأن يتكرر نمط تصميم معين في جميع أنحاء الصفحة بتكرار القيم التي قمت بتخصيصها في جانب من جوانب التصميم مثل الألوان، الإطارات ذات الزوايات المنحنية (border radius), الظلال (box shadows)، ومقاسات الهوامش الخارجية (margins). أي أن كثيرٌ من التنسيقات المحلية (localized styles) ستأخذ بالعمل القائم بالفعل للتنسيقات العمومية (global styles) التي قمت بتخصيصها بالأعلى.

السبب الثاني، والأكثر غموضًا، وهو أن الأسلوب الذي تتبعه CSS وأسلوبك في اتخاذ قررات التصيمم يتأثران بالسياق المحيط بالصفحة. مثلا، فكّر في تطبيق الكود التالي على عنصر ما داخل الصفحة:

``` css
.the-thing {
  position: absolute;
  top: 10px;
  left: 10px;
}
```

ما الذي سيقوم بفعله هذا الكود؟ بدون معرفة موقع العنصر في بنية الصفحة "DOM"، وما هي التنسيقات الأخرى التي طُبقت لباقي عناصر الصفحة؛ فإنه لا توجد طريقة لمعرفة ذلك. إن الوضع المطلق (Absolute Positioning) يُطبّق ويُشبك مع أقرب عنصر أب أو جد يمتلك الوضع النسبي (Relative Positioning)؛ لذا فإن تطبيق خاصية الوضع المطلق هنا في هذا المثال، يعني أشياء عديدة معتمدة على أي واحد من تلك العناصر الآباء أو الأجداد، إن وُجد، يمتلك الخاصية `position: relative`.

علاوة على ذلك، طريقة تَمكُنك (أو عدم تمكنك) من وضع عنصر أمام الآخر بشكل متراص سوف تأخذك للإعتماد بشكل كبير على موقع هذين العنصرين في بنية الصفحة "DOM". والتبديل بين العناصر في الـ "DOM" قد يسبب تأثيرات جذرية وهائلة في الطريقة التي تتهيأ بها تلك العناصر لتتناسب مع بعضها البعض ويأخذ كل عنصر موقعه وترتيبه. وهذا هو ما يجعل انسياب الصفحة وترتيب وتراص السياقات (contexts) موضوعات غاية في الأهمية، وفي أحيان أخرى موضوعات شائكة وغاية في التعقيد.

والطبيعة السياقية للغة CSS هي أيضًا تعود جزئيًا إلى الطريقة التي يعمل بها التصميم. فلو أن هناك مهندس يصمم جسر، لا يمكنك أن تنظر فقط في مخطط العمل وتقول: "إن كل شيء على ما يرام عدا تلك "الكمرة" التي تحمل الجسر هنا؛ عليك أن تتخلص منها". إزالة تلك "الكمرة" يترتب عليها عواقب تنعكس على سلامة البنية الهيكلية والتكامل التركيبي للجسر بأكلمه! وعلى نحو مماثل في التصميم، فإن تغيير أو إزالة أحد أجزاء أو عناصر تصميم ما، من الممكن أن يليه عواقب تنعكس على الطريقة التي تظهر بها باقي العناصر على الشاشة. وفي أحيانٍ كثيرة سوف تحتاج إلى تخصيص تنسيقات لأكثر من عنصر معًا، بشكل مترابط ومتلازم! (بمعنى أنه سيكون لديك عناصر قائمة على/ ومرتبطة بتنسيقات مشتركة ولا يمكن الفصل بين أحدها أو تغيير شيء ما إلا وقد يترتب على ذلك عواقب أخرى تنعكس على باقي العناصر).

على سبيل المثال، لو جعلت العنوان الرئيسي كبيرًا جدًا في لوحة ما داخل التصميم؛ فإنه سيصبح بارزًا للغاية في وجه المستخدم وبالتالي سيتسبب في جعل باقي العناصر على الشاشة تبدو وكأنها مهملة وأقل في الأهمية. والقيود هنا لا تدور حول الفيزياء كما هو الحال مع الجسر في المثال السابق، ولكن هناك مباديء وقواعد غامضة لما يسمى بـ "العلوم الناعمة" والتي تؤثر على الادراك والتصور لدى البشر. لذا، فإن أجزاء الصفحة التي تُعالج (render) لتظهر في مكان مادي-فيزيائي على الشاشة، وحقائق العالم المادي-الفيزيائي (وكيف أننا ندركه ونتصوره) هي أمور بالغة الأهمية علينا أنه ننتبه إليها جيدًا.

نحن نفضل تصميم البرمجيات باستخدام [مبادي قابلية التركيب والتقسيم إلى وحدات، والكبسلة](https://freecontent.manning.com/modular-css/) (Modularity and Encapsulation). ذلك يجعل الأمر منطقيًا في عالم الكود، لأن الكود مصحوب بالتعقيدات، وانتهاج تلك المباديء يساعدنا على تقسيم المشكلة إلى أجزاء مقدور عليها ويسهل التعامل معها. لكن ينبغي أيضًا أن نكون مدركين أنه من الممكن ألا يكون هذا مثاليًا طوال الوقت؛ فنحن لا نستطيع أبدًا، في CSS، أن نهمل ونتجاهل بشكل كامل ما يحدث خارج وحدة ما (module) مُعطاه.

## الخلاصة
هذه الجوانب الثلاثة تجعل CSS لغة مختلفة عن باقي لغات البرمجة التلقليدية. وهذه الإختلافات يمكن أن تبدو غير مألوفة، لكنها تجعل من CSS لغة متينة وقوية. وفي ظني أن المطورين الذين يُعطون الإهتمام لتلك الأمور مُحاولين فهمها واستيعابها بشكل كامل؛ يُصبحوا مؤهلين لِأن يكونوا أكثر احترافية في استخدام CSS.

- ترجمة بتصرف لمقال :([Resilient, Declarative, Contextual](https://keithjgrant.com/posts/2018/06/resilient-declarative-contextual/)), للكاتب: [كيث ج. جرانت](https://twitter.com/keithjgrant)، بإذن مسبق منه.