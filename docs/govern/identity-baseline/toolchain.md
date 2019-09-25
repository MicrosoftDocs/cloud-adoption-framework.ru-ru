---
title: Средства основных способов идентификации в Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Средства основных способов идентификации в Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 72060f16add37d62a4747c5fe9d5aef49fe04c58
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222118"
---
# <a name="identity-baseline-tools-in-azure"></a>Средства основных способов идентификации в Azure

[Основные способы идентификации](./index.md) — это одна из [пяти дисциплин системы управления облаком](../governance-disciplines.md). Эта дисциплина посвящена способам создания политик, гарантирующих согласованность и непрерывность идентификаторов пользователей, независимо от поставщика облачных служб, который размещает приложение или рабочую нагрузку.

В руководство по обнаружению гибридного удостоверения включены следующие средства.

**Доменные службы Active Directory (локальные)** . Доменные службы Active Directory — это поставщик удостоверений, наиболее часто используемый на предприятии для хранения и проверки учетных данных пользователя.

**Azure Active Directory:** Программное обеспечение как услуга (SaaS), эквивалентное Active Directory, поддерживает федерацию с локальными доменными службами Active Directory.

**Доменные службы Active Directory (IaaS)** . Экземпляр приложения доменных служб Active Directory, запущенных на виртуальной машине в Azure.

Идентификатор представляет собой новую плоскость управления в сфере ИТ-безопасности. Поэтому проверка подлинности — это защитник доступа к организации в облаке. Организации должны определить плоскость управления удостоверениями, которая повышает безопасность и защищает облачные приложения от несанкционированного доступа.

## <a name="cloud-authentication"></a>Облачная аутентификация

Выбор правильного метода аутентификации является первой задачей для организаций, которые хотят переместить свои приложения в облако.

При выборе этого метода Azure AD обрабатывает процесс входа пользователей. В сочетании с простым единым входом (SSO) пользователи могут войти в облачные приложения без необходимости повторного ввода своих учетных данных. При использовании облачной аутентификации вы можете выбрать один из двух вариантов:

**Синхронизация хэша паролей Azure AD:** Это самый простой способ включить аутентификацию объектов локального каталога в Azure AD. Этот метод также можно использовать с любым методом в качестве резервного метода проверки подлинности в случае отказа локального сервера.

**Сквозная проверка подлинности Azure AD:** Обеспечивает постоянную проверку пароля для служб проверки подлинности Azure AD с помощью программного агента, выполняемого на одном или нескольких локальных серверах.

> [!NOTE]
> Этот метод сквозной проверки подлинности следует использовать организациям с требованием безопасности, предписывающим немедленное применение состояний локальных учетных записей пользователей, политик паролей и времени входа.

**Федеративная проверка подлинности**.

При выборе этого метода Azure AD передает процесс проверки подлинности отдельной доверенной системе проверки подлинности, например локальным службам федерации Active Directory (AD FS) или доверенному стороннему поставщику федерации, для проверки пароля пользователя.

Статья [Выбор правильного метода аутентификации для гибридного решения для идентификации Azure Active Directory](https://docs.microsoft.com/azure/security/azure-ad-choose-authn) содержит дерево принятия решений, которое поможет вам выбрать лучшее решение для вашей организации.

Ниже указана таблица со списком собственных средств Azure, которые могут помочь в совершенствовании политик и процессов, поддерживающих эту дисциплину управления.

<!-- markdownlint-disable MD033 -->

|Рассматриваемый вопрос|Синхронизация хэша паролей и простой единый вход|Сквозная аутентификация и простой единый вход|Федерация с AD FS|
|:-----|:-----|:-----|:-----|
|Где происходит аутентификация?|В облаке|В облаке после безопасного обмена данными проверки пароля с локальным агентом аутентификации|Локальная система|
|Каковы требования к локальному серверу, помимо системы подготовки: Azure AD Connect?|Отсутствуют|Один сервер для каждого дополнительного агента аутентификации|Не менее двух серверов AD FS<br><br>Не менее двух WAP-серверов в сети периметра|
|Каковы требования к локальному Интернету и сети за пределами системы подготовки?|Отсутствуют|[Исходящий доступ в Интернет](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-quick-start) с серверов, на которых выполняются агенты проверки подлинности|[Входящий доступ в Интернет](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/ad-fs-requirements) к серверам WAP в периметре<br><br>Входящий сетевой доступ к серверам AD FS с WAP-серверов в сети периметра<br><br>Балансировка сетевой нагрузки|
|Существует ли требование к SSL-сертификату?|Нет|Нет|Да|
|Имеется ли решение для мониторинга работоспособности?|Не требуется|Состояние агента, предоставляемое [Центром администрирования Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/tshoot-connect-pass-through-authentication)|[Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-health-adfs)|
|Пользователи получают единый вход в облачные ресурсы с присоединенных к домену устройств в корпоративной сети?|Да, с [простым единым входом](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)|Да, с [простым единым входом](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)|Да|
|Какие типы входа поддерживаются?|UserPrincipalName и пароль<br><br>Встроенная проверка подлинности Windows с [простым единым входом](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)<br><br>[Альтернативный идентификатор входа](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-custom)|UserPrincipalName и пароль<br><br>Встроенная проверка подлинности Windows с [простым единым входом](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)<br><br>[Альтернативный идентификатор входа](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-faq)|UserPrincipalName и пароль<br><br>sAMAccountName и пароль<br><br>Встроенная проверка подлинности Windows<br><br>[Аутентификация с использованием сертификатов и смарт-карт](/windows-server/identity/ad-fs/operations/configure-user-certificate-authentication)<br><br>[Альтернативный идентификатор входа](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)|
|Поддерживается ли Windows Hello для бизнеса?|[Модель доверия на основе ключей](/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Модель доверия на основе сертификатов с Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Модель доверия на основе ключей](/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Модель доверия на основе сертификатов с Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Модель доверия на основе ключей](/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Модель доверия на основе сертификатов](/windows/security/identity-protection/hello-for-business/hello-key-trust-adfs)|
|Какие варианты многофакторной идентификации существуют?|[Многофакторная идентификация Azure](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Пользовательские элементы управления для функции условного доступа*](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Многофакторная идентификация Azure](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Пользовательские элементы управления для функции условного доступа*](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Многофакторная идентификация Azure](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Сервер многофакторной идентификации Azure](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfaserver-deploy)<br><br>[Сторонняя многофакторная идентификация](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)<br><br>[Пользовательские элементы управления для функции условного доступа*](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|
|Какие состояния учетной записи пользователя поддерживаются?|Отключенные учетные записи<br>(до 30-минутной задержки)|Отключенные учетные записи<br><br>Учетная запись заблокирована<br><br>Срок действия учетной записи истек.<br><br>Срок действия пароля истек<br><br>Время входа|Отключенные учетные записи<br><br>Учетная запись заблокирована<br><br>Срок действия учетной записи истек.<br><br>Срок действия пароля истек<br><br>Время входа|
|Какие варианты условного доступа поддерживаются?|[Условный доступ Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Условный доступ Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Условный доступ Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)<br><br>[Правила утверждений AD FS](https://adfshelp.microsoft.com/AadTrustClaims/ClaimsGenerator)|
|Поддерживается ли блокировка устаревших протоколов?|[Да](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Да](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Да](/windows-server/identity/ad-fs/operations/access-control-policies-w2k12)|
|Можно ли настроить логотип, изображение и описание на страницах входа?|[Да, в Azure AD Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Да, в Azure AD Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Да](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#customlogo)|
|Какие дополнительные сценарии поддерживаются?|[Интеллектуальная блокировка паролей](https://docs.microsoft.com/azure/active-directory/active-directory-secure-passwords)<br><br>[Отчеты об утерянных учетных данных](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-risk-events)|[Интеллектуальная блокировка паролей](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-smart-lockout)|Система аутентификации нескольких сайтов с низкой задержкой<br><br>[Блокировка экстрасети AD FS](/windows-server/identity/ad-fs/operations/configure-ad-fs-extranet-soft-lockout-protection)<br><br>[Интеграция со сторонними системами идентификации](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-compatibility)|

<!-- markdownlint-enable MD033 -->

> [!NOTE]
> Пользовательские элементы управления в компоненте условного доступа Azure AD сейчас не поддерживают регистрацию устройств.

## <a name="next-steps"></a>Следующие шаги

В [техническом документе об инфраструктуре цифрового преобразования удостоверений](https://resources.office.com/ww-landing-M365E-EMS-IDAM-Hybrid-Identity-WhitePaper.html?LCID=EN-US) описаны сочетания и решения для выбора и интеграции каждого из этих компонентов.

Средство [Azure AD Connect](https://aka.ms/aadconnectwiz) позволяет интегрировать локальные каталоги с Azure AD.
