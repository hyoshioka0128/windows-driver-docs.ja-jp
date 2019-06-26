---
title: プロパティ ページの拡張 Dll の要件
description: デバイスのプロパティ ページのプロバイダーの一般的な要件 (プロパティ ページの拡張 DLL)
ms.assetid: bc48d848-a216-442e-97ca-f990f8d243ac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2bb049acf85ad490d152ea43e38f750cadd6f2b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385889"
---
# <a name="specific-requirements-for-device-property-page-providers-property-page-extension-dlls"></a>デバイスのプロパティ ページのプロバイダーの一般的な要件 (プロパティ ページの拡張 DLL)


このトピックで作成し、プロパティ ページの拡張 DLL をインストールする方法。

### <a name="creating-a-property-page-extension-dll"></a>プロパティ ページの拡張 dll の作成

プロパティ ページの拡張カスタム プロパティ ページを提供する DLL は、プロパティ ページを追加する要求を処理する必要があります。 この要求が行われる、 **AddPropSheetPageProc**コールバック関数。

この要求に応答してで、DLL は各カスタム プロパティ ページの情報を提供します、ページを作成し、デバイスの動的プロパティ ページの一覧に、作成したページを追加します。

プロパティ ページの拡張 DLL でカスタム デバイスのプロパティ ページを作成する方法については、次を参照してください。[デバイスのプロパティ ページのプロバイダーの一般的な要件](general-requirements-for-device-property-page-providers.md)します。

### <a name="installing-a-device-property-page"></a>デバイスのプロパティ ページのインストール

次のディレクティブを使用して DLL がインストールされているプロパティ ページの拡張機能、 [INF ファイル](overview-of-inf-files.md)の[ドライバー パッケージ](driver-packages.md):

1.  使用して、*追加レジストリ セクション*で指定される、 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)で、 [ **INF *DDInstall*セクション**](inf-ddinstall-section.md)、追加する、 **EnumPropPages32**デバイスのエントリ。 **EnumPropPages32**エントリは、次を指定[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)値。

    -   エクスポートする DLL の名前、 **ExtensionPropSheetPageProc**コールバック関数。
    -   名前、 **ExtensionPropSheetPageProc** DLL によって実装されるコールバック関数。

    次のコード例は、*追加レジストリ セクション*を追加する、 **EnumPropPages32** DLL の名前を指定するエントリ (*MyPropProvider.dll*) とコールバック関数 (*MyCallbackFunction*)。

    ```cpp
    HKR, , EnumPropPages32, 0, "MyPropProvider.dll, MyCallbackFunction"
    ```

    **重要な**  の DLL とコールバック関数名の両方をまとめて引用符で囲む必要があります ("")。

     

2.  含める、 [ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)プロパティ ページの拡張 DLL をコピーするに、 *%systemroot%\\System32*ディレクトリ。

3.  デバイスがネットワーク アダプターの場合は、いずれかとして NCF_HAS_UI を指定する必要があります、**特性**値、 [ **INF DDInstall セクション**](inf-ddinstall-section.md)します。 この値は、アダプターがユーザー インターフェイスをサポートしていることを示します。

    詳細については、次を参照してください。[ネットワーク アダプターのカスタム プロパティ ページを指定する](https://docs.microsoft.com/windows-hardware/drivers/network/specifying-custom-property-pages-for-network-adapters)します。

 

 





