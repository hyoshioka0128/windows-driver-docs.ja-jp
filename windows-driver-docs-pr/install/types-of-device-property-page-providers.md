---
title: デバイスのプロパティ ページのプロバイダーの種類
description: デバイスのプロパティ ページのプロバイダーの種類
ms.assetid: b467543e-6907-44e5-b407-637cad7f6d78
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af1afea7fd441c22586a56ed4570b33fc5e984c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370926"
---
# <a name="types-of-device-property-page-providers"></a>デバイスのプロパティ ページのプロバイダーの種類


次の種類のプロパティ ページのプロバイダーを使用して、カスタム デバイスのプロパティ ページを指定できます。

-   **クラスのインストーラーと共同インストーラー。**

    A[共同インストーラー](writing-a-co-installer.md)サポートすることで 1 つまたは複数のデバイスのカスタム プロパティ ページを提供することができます、 [ **DIF_ADDPROPERTYPAGE_ADVANCED** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-addpropertypage-advanced)デバイス インストール機能 (差分) コード。 プロパティを提供するインストーラーがハンドルをページと、 **DIF_ADDPROPERTYPAGE_ADVANCED**要求、プロパティ ページ ダイアログ ボックス プロシージャのアドレスを設定します。

    Windows Driver Kit (WDK) でトースター サンプルの一部である共同インストーラーには、この種類のデバイスのプロパティ ページのプロバイダーがサポートしています。 ある、 *src\\全般\\トースター\\classinstaller* WDK のサブディレクトリ。

    この種類のプロバイダーの要件の詳細については、次を参照してください。[デバイス プロパティ ページのプロバイダー (共同インストーラー) の特定の要件](specific-requirements-for-device-property-page-providers--class-instal.md)します。

    **注**  一般に他の特定のデバイスまたはデバイス固有クラスとの共同インストーラーでこの機能を提供することをお勧めカスタム デバイスのプロパティ ページを提供するクラスのインストーラーを作成できますが機能です。

     

-   **プロパティ ページの拡張 DLL。**

    1 つまたは複数のデバイスのカスタム プロパティ ページを提供する DLL と呼ばれます、*プロパティ ページの拡張 DLL*します。 この種類のプロバイダーは、実装することによってカスタム プロパティ ページをサポートしています、 **AddPropSheetPageProc、ExtensionPropSheetPageProc**、およびその他のプロパティ シートのコールバック関数。 これらの関数の詳細については、Microsoft Windows ソフトウェア開発キット (SDK) for Windows 7 および .NET Framework 4.0 のドキュメントを参照してください。

    指定することでこの種類のプロバイダーがインストールされている、 **EnumPropPages32**内のエントリ、*追加レジストリ セクション*の[ **INF AddReg ディレクティブ**](inf-addreg-directive.md). 内でこのディレクティブが指定されて、 [ **INF *DDInstall*セクション**](inf-ddinstall-section.md)します。

    AC97 サンプル オーディオ ドライバーには、この種類のデバイスのプロパティ ページのプロバイダーがサポートしています。 ある、 *src\\オーディオ\\ac97* WDK のサブディレクトリ。

    この種類のプロバイダーの要件の詳細については、次を参照してください。[デバイス プロパティ ページのプロバイダー (プロパティ ページの拡張 Dll) の特定の要件](specific-requirements-for-device-property-page-providers--property-pag.md)します。

    **注**  しない限り、[ドライバー パッケージ](driver-packages.md)クラス インストーラーまたは共同インストーラーを必要とプロパティ ページの拡張 DLL を使用してカスタムのデバイスのプロパティ ページをサポートする方が効率的です。

     

すべての種類のデバイスのプロパティ ページのプロバイダーがで説明されているガイドラインに従う必要があります[デバイスのプロパティ ページのプロバイダーの一般的な要件](general-requirements-for-device-property-page-providers.md)します。

 

 





