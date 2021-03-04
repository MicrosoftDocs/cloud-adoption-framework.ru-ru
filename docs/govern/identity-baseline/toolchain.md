---
title: Средства основных способов идентификации в Azure
description: Узнайте, как собственные средства Azure могут помочь развитым политикам и процессам, поддерживающим дисциплину базовых показателей идентификаторов.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: internal
ms.openlocfilehash: 0ff9bb28035982564accac23c15cec1fe9133c47
ms.sourcegitcommit: b8f8b7631aabaab28e9705934bf67dad15e3a179
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/03/2021
ms.locfileid: "101792454"
---
# <a name="identity-baseline-tools-in-azure"></a>Средства основных способов идентификации в Azure

[Дисциплина базовых показателей](./index.md) является одной из [пяти дисциплин управления облаком](../governance-disciplines.md). Эта дисциплина посвящена способам создания политик, гарантирующих согласованность и непрерывность идентификаторов пользователей, независимо от поставщика облачных служб, который размещает приложение или рабочую нагрузку.

Следующие средства включены в руководством по обнаружению гибридной идентификации.

**Active Directory (локально):** Active Directory — это поставщик удостоверений, наиболее часто используемый в Организации для хранения и проверки учетных данных пользователя.

**Azure Active Directory:** Программное обеспечение как услуга (SaaS), эквивалентное Active Directory, которое поддерживает федерацию с локальной Active Directory.

**Active Directory (IaaS):** Экземпляр Active Directory приложения, работающего на виртуальной машине в Azure.

Идентификатор представляет собой новую плоскость управления в сфере ИТ-безопасности. Поэтому проверка подлинности — это защита доступа Организации к облаку. Организациям требуется плоскость управления удостоверениями, которая обеспечивает безопасность и защиту облачных приложений от злоумышленников.

## <a name="cloud-authentication"></a>Облачная аутентификация

Выбор правильного метода проверки подлинности является первой проблемой для организаций, желающих переместить свои приложения в облако.

При выборе этого метода Azure AD обрабатывает процесс входа пользователей. В сочетании с простым единым входом (SSO) пользователи могут входить в облачные приложения без необходимости повторно вводить учетные данные. При использовании облачной аутентификации вы можете выбрать один из двух вариантов:

**Синхронизация хэша паролей Azure AD:** Самый простой способ включить проверку подлинности для локальных объектов каталога в Azure AD. Этот метод также можно использовать с любым методом в качестве резервного метода проверки подлинности в случае отказа локального сервера.

**Сквозная проверка подлинности Azure AD:** Обеспечивает постоянную проверку пароля для служб проверки подлинности Azure AD с помощью агента программного обеспечения, работающего на одном или нескольких локальных серверах.

<!-- docutune:casing "the pass-through authentication method" -->

> [!NOTE]
> Компании с требованием безопасности для немедленного применения локальных состояний учетных записей пользователей, политик паролей и часов входа должны учитывать метод сквозной проверки подлинности.

**Федеративная аутентификация:**

При выборе этого метода Azure AD передает процесс проверки подлинности в отдельную доверенную систему проверки подлинности, например локальную службы федерации Active Directory (AD FS) (AD FS) или доверенный сторонний поставщик Федерации, для проверки пароля пользователя.

Сведения о дереве принятия решений, помогающем выбрать лучшее решение для вашей организации, см. [в разделе Выбор правильного метода проверки подлинности для Azure Active Directory](/azure/active-directory/hybrid/choose-ad-authn).

В следующей таблице перечислены собственные средства, которые могут помочь развитым политикам и процессам, поддерживающим эту дисциплину.

<!-- docutune:casing UserPrincipalName SamAccountName "conditional access options" -->

| Рассматриваемый вопрос | Синхронизация хэша паролей и простой единый вход | Сквозная аутентификация и простой единый вход | Федерация с AD FS |
| --- | --- | --- | --- |
| Где происходит аутентификация? | В облаке | В облаке после безопасного обмена данными проверки пароля с локальным агентом аутентификации | В локальной среде |
| Каковы требования к локальному серверу, помимо системы подготовки: Azure AD Connect? | None | Один сервер для каждого дополнительного агента аутентификации | Не менее двух серверов AD FS <br><br> Два или более серверов WAP в сети периметра |
| Каковы требования к локальному Интернету и сети за пределами системы подготовки? | None | [Исходящий доступ в Интернет](/azure/active-directory/hybrid/how-to-connect-pta-quick-start) с серверов, на которых выполняются агенты проверки подлинности | [Входящий доступ в Интернет](/windows-server/identity/ad-fs/overview/ad-fs-requirements) к серверам WAP в периметре <br><br> Входящий сетевой доступ к серверам AD FS с WAP-серверов в сети периметра <br><br> Балансировка сетевой нагрузки |
| Существует ли требование к SSL-сертификату? | Нет | Нет | Да |
| Имеется ли решение для мониторинга работоспособности? | Не требуется | Состояние агента, предоставляемое [Центром администрирования Azure Active Directory](/azure/active-directory/hybrid/tshoot-connect-pass-through-authentication#general-issues) | [Azure AD Connect Health](/azure/active-directory/hybrid/how-to-connect-health-adfs) |
| Пользователи получают единый вход в облачные ресурсы с присоединенных к домену устройств в корпоративной сети? | Да, с [простым единым входом](/azure/active-directory/hybrid/how-to-connect-sso) | Да, с [простым единым входом](/azure/active-directory/hybrid/how-to-connect-sso) | Да |
| Какие типы входа поддерживаются? | UserPrincipalName и пароль <br><br> Встроенная проверка подлинности Windows с помощью [простого единого входа](/azure/active-directory/hybrid/how-to-connect-sso) <br><br> [Альтернативный идентификатор входа](/azure/active-directory/hybrid/how-to-connect-install-custom) | UserPrincipalName и пароль <br><br> Встроенная проверка подлинности Windows с помощью [простого единого входа](/azure/active-directory/hybrid/how-to-connect-sso) <br><br> [Альтернативный идентификатор входа](/azure/active-directory/hybrid/how-to-connect-pta-faq) | UserPrincipalName и пароль <br><br> SamAccountName + Password <br><br> Встроенная проверка подлинности Windows <br><br> [Аутентификация с использованием сертификатов и смарт-карт](/windows-server/identity/ad-fs/operations/configure-user-certificate-authentication) <br><br> [Альтернативный идентификатор входа](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) |
| Поддерживается ли Windows Hello для бизнеса? | [Модель доверия на основе ключей](/windows/security/identity-protection/hello-for-business/hello-identity-verification) <br><br> [Модель доверия на основе сертификатов с Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune/) | [Модель доверия на основе ключей](/windows/security/identity-protection/hello-for-business/hello-identity-verification) <br><br> [Модель доверия на основе сертификатов с Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune/) | [Модель доверия на основе ключей](/windows/security/identity-protection/hello-for-business/hello-identity-verification) <br><br> [Модель доверия на основе сертификатов](/windows/security/identity-protection/hello-for-business/hello-key-trust-adfs) |
| Какие варианты многофакторной идентификации существуют? | [Многофакторная идентификация Azure](/azure/active-directory/authentication/) <br><br> [Настраиваемые элементы управления с условным доступом Azure AD *](/azure/active-directory/conditional-access/controls#custom-controls-preview) | [Многофакторная идентификация Azure](/azure/active-directory/authentication/) <br><br> [Настраиваемые элементы управления с условным доступом Azure AD *](/azure/active-directory/conditional-access/controls#custom-controls-preview) | [Многофакторная идентификация Azure](/azure/active-directory/authentication/) <br><br> [Сервер многофакторной идентификации Azure](/azure/active-directory/authentication/howto-mfaserver-deploy) <br><br> [Сторонняя многофакторная идентификация](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs) <br><br> [Пользовательские элементы управления с доступом к Azure AD](/azure/active-directory/conditional-access/controls#custom-controls-preview) |
| Какие состояния учетной записи пользователя поддерживаются? | Отключенные учетные записи <br> (До 30-минутной задержки) | Отключенные учетные записи <br><br> Учетная запись заблокирована <br><br> Срок действия учетной записи истек <br><br> Срок действия пароля истек <br><br> Время входа | Отключенные учетные записи <br><br> Учетная запись заблокирована <br><br> Срок действия учетной записи истек <br><br> Срок действия пароля истек <br><br> Время входа |
| Каковы параметры условного доступа в Azure AD? | [Условный доступ Azure AD](/azure/active-directory/conditional-access/overview) | [Условный доступ Azure AD](/azure/active-directory/conditional-access/overview) | [Условный доступ Azure AD](/azure/active-directory/conditional-access/overview) <br><br> [Правила утверждений AD FS](https://adfshelp.microsoft.com/AadTrustClaims/ClaimsGenerator) |
| Поддерживается ли блокировка устаревших протоколов? | [Да](/azure/active-directory/fundamentals/concept-fundamentals-security-defaults) | [Да](/azure/active-directory/fundamentals/concept-fundamentals-security-defaults) | [Да](/windows-server/identity/ad-fs/operations/access-control-policies-w2k12) |
| Можно ли настроить логотип, изображение и описание на страницах входа? | [Да, в Azure AD Premium](/azure/active-directory/fundamentals/customize-branding) | [Да, в Azure AD Premium](/azure/active-directory/fundamentals/customize-branding) | [Да](/azure/active-directory/hybrid/how-to-connect-fed-management#customlogo) |
| Какие дополнительные сценарии поддерживаются? | [Интеллектуальная блокировка паролей](/azure/active-directory/authentication/concept-sspr-howitworks) <br><br> [Отчеты об утерянных учетных данных](/azure/active-directory/identity-protection/overview-identity-protection) | [Интеллектуальная блокировка паролей](/azure/active-directory/authentication/howto-password-smart-lockout) | Система аутентификации нескольких сайтов с низкой задержкой <br><br> [Блокировка экстрасети AD FS](/windows-server/identity/ad-fs/operations/configure-ad-fs-extranet-soft-lockout-protection) <br><br> [Интеграция со сторонними системами идентификации](/azure/active-directory/hybrid/how-to-connect-fed-compatibility) |

> [!NOTE]
> Настраиваемые элементы управления в условном доступе Azure AD в настоящее время не поддерживают регистрацию устройств.

## <a name="next-steps"></a>Дальнейшие действия

<!-- TODO: The download button for this whitepaper returns 404. -->

<!-- docutune:casing "Hybrid Identity Digital Transformation Framework" -->

В [техническом документе об инфраструктуре цифрового преобразования для гибридной идентификации](https://resources.office.com/ww-landing-M365E-EMS-IDAM-Hybrid-Identity-WhitePaper.html) приведены сочетания и решения для выбора и интеграции каждого из этих компонентов.

Средство [Azure AD Connect](https://aka.ms/aadconnectwiz) позволяет интегрировать локальные каталоги с Azure AD.
