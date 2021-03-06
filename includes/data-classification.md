<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD026 MD041 -->
Классификация данных позволяет определить и назначить данные организации и предоставляет общую отправную точку для управления. Процесс классификации данных распределяет данные по конфиденциальности и бизнес-влиянию для обнаружения рисков. Если данные классифицируются, вы можете управлять ими способами, которые защищают конфиденциальные или важные данные от кражи или потери.

## <a name="understand-data-risks-then-manage-them"></a>Изучите риски с данными, а затем управляйте ими

Прежде чем можно будет управлять риском, его необходимо понять. В случае ответственности за нарушение безопасности данных такое распознавание начинается с классификации данных. Классификация данных — это процесс связывания характеристик метаданных с каждым ресурсом в цифровом расположении, который определяет тип данных, связанных с этим ресурсом.

Любой ресурс, идентифицированный как потенциальный кандидат на миграцию или развертывание в облаке, должен иметь документированные метаданные для записи классификации данных, критических бизнес-процессов и ответственности за выставление счетов. Эти три точки классификации могут иметь большое значение для распознавания и устранения рисков.

## <a name="classifications-microsoft-uses"></a>Классификации, используемые корпорацией Майкрософт

Ниже приведен список классификаций, используемых корпорацией Майкрософт. В зависимости от отрасли или существующих требований безопасности стандарты классификации данных могут уже существовать в вашей организации. Если ни один стандарт не существует, можно использовать этот пример классификации, чтобы лучше понять свой профиль цифровой Организации и риска.

- **Не для бизнеса:** Данные из личной жизни, которые не принадлежат корпорации Майкрософт.
- **Общедоступная:** Бизнес-данные, которые свободно доступны и утверждаются для общедоступного потребления.
- **Общие сведения:** Бизнес-данные, не предназначенные для общедоступной аудитории.
- **Конфиденциально:** Бизнес-данные, которые могут причинить вред корпорации Майкрософт, если они имеют общий доступ.
- **Строго конфиденциально:** Бизнес-данные, которые могут привести к серьезному вреду корпорации Майкрософт в случае их перераспределения.

## <a name="tagging-data-classification-in-azure"></a>Добавление тегов к классификации данных в Azure

Теги ресурсов — хороший подход к хранению метаданных, и эти теги можно использовать для применения сведений о классификации данных к развернутым ресурсам. Хотя Теги облачных ресурсов по классификации не являются заменой для процесса формальной классификации данных, он предоставляет ценное средство для управления ресурсами и применения политик. [Azure Information Protection](/azure/information-protection/what-is-information-protection) — отличное решение, помогающее классифицировать сами данные, независимо от того, где они находятся (локально, в Azure или где-либо еще). Рассмотрите его как часть общей стратегии классификации.

## <a name="take-action"></a>Выполнить действие

Выполните действия, определив и размечая ресурсы, используя определенную классификацию данных.

- [Выберите один из руководств по управлению действиями,](../docs/govern/guides/index.md) чтобы получить примеры применения тегов в портфеле.
- Ознакомьтесь с [рекомендуемыми соглашениями об именовании и маркировке](../docs/ready/azure-best-practices/resource-tagging.md) , чтобы определить более полный стандарт тегов.
- Дополнительные сведения о разметке ресурсов в Azure см. в статье [Использование тегов для Организации ресурсов Azure и иерархии управления](/azure/azure-resource-manager/management/tag-resources).
