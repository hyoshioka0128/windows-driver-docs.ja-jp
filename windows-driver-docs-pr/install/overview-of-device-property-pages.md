---
title: デバイスのプロパティ ページの概要
description: デバイスのプロパティ ページの概要
ms.assetid: b117721a-db32-4144-b0ae-5a0fca40f9db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec451c9885886f57c61489a7727a1f093daf8d53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369448"
---
# <a name="overview-of-device-property-pages"></a>デバイスのプロパティ ページの概要


A*デバイス プロパティ ページ*は、ユーザーを表示およびデバイスのプロパティを編集できるウィンドウです。 ほとんどのデバイスのオペレーティング システムは、ユーザーを表示して、そのデバイスのパラメーターの共通セットの編集を許可する標準的なデバイス プロパティのページを提供します。 デバイスのプロパティ ページを表示する方法の詳細については、次を参照してください。[プロパティ ページをどのデバイスが表示される](how-device-property-pages-are-displayed.md)します。

独立系ハードウェア ベンダー (Ihv) は、通常、ユーザーを表示して、デバイスの追加と独自のプロパティの編集を許可するカスタム デバイスのプロパティ ページを提供します。 これらのプロパティは、IHV を提供する各デバイスに固有です。 これらのプロパティは、CD ドライブの既定の再生のボリュームまたはモデムのスピーカーの音量などがあります。

IHV は、プロパティ ページのプロバイダーを使用して、カスタムのデバイスのプロパティ ページを作成します。 プロパティ ページのプロバイダーには、次のいずれかを指定できます。

<a href="" id="class-installers-and-co-installers"></a>**クラスのインストーラーと共同インストーラー**  
共同インストーラーまたはクラスのインストーラーは、DIF_ADDPROPERTYPAGE_ADVANCED デバイスのインストール機能 (差分) コードをサポートすることで、1 つまたは複数のデバイスのカスタム プロパティ ページを提供できます。

<a href="" id="property-page-extension-dll"></a>**プロパティ ページの拡張 DLL**  
1 つまたは複数のデバイスのカスタム プロパティ ページを提供するダイナミック リンク ライブラリ (DLL) と呼びます、*プロパティ ページの拡張 DLL*します。 この種類のプロバイダーは、実装することによってカスタム プロパティ ページをサポートしています、 **AddPropSheetPageProc**、 **ExtensionPropSheetPageProc**、およびその他のプロパティ シートのコールバック関数。

これらの関数の詳細については、Windows 7 および .NET Framework 4.0 用 Microsoft Windows ソフトウェア開発キット (SDK) を参照してください。

IHV は、そのデバイスまたはデバイス クラスにユーザーが設定できる個々 のプロパティがある場合、ドライバー パッケージのプロパティ ページのカスタム デバイスのプロバイダーを指定します。

**注**  Windows 2000 より前のバージョンの Windows でユーザーがコントロール パネルでこのような情報を設定します。 Windows 2000 および Windows の以降のバージョン用に記述されたドライバー ソフトウェアは、代わりにプロパティ ページを指定する必要があります。

 

プロパティ ページのプロバイダーの詳細については、次を参照してください。[デバイス プロパティ ページ プロバイダーの種類](types-of-device-property-page-providers.md)します。

Windows SDK for Windows 7 および .NET Framework 4.0 のドキュメントでは、プロパティ ページとそれらを操作する Microsoft Win32 関数についての包括的なガイダンスを提供します。 プロパティ ページやプロパティ シートに関する詳細については、次を参照してください。[プロパティ シート](https://go.microsoft.com/fwlink/p/?linkid=180781)、Windows SDK for Windows 7 および .NET Framework 4.0 のドキュメントにします。

 

 





