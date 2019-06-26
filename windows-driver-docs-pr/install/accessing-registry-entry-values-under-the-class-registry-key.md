---
title: クラスのレジストリ キーの下のレジストリ エントリ値へのアクセス
description: クラスのレジストリ キーの下のレジストリ エントリ値へのアクセス
ms.assetid: 771b5751-db9f-43fa-90d1-1c43918a3a80
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3152632f359ff866192e58150fb3fc42ae5e1124
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386048"
---
# <a name="accessing-registry-entry-values-under-the-class-registry-key"></a>クラスのレジストリ キーの下のレジストリ エントリ値へのアクセス


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)が含まれています[デバイス セットアップ クラスのプロパティ](accessing-device-setup-class-properties.md)対応する SPCRP_ を持たない*Xxx*識別子。 これらのプロパティには、デバイス セットアップ クラスが特徴付けられます。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 もこれらのデバイス セットアップ クラスのプロパティのほとんどをサポートします。 ただし、Windows の以前のバージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 代わりに、これらのバージョンの Windows では、クラスのレジストリ キーの下の対応するシステム定義のレジストリ エントリ値を使用してこれらのプロパティを表します。 Windows の以前のバージョンとの互換性を維持するために Windows Vista およびそれ以降のバージョンもサポートしてこれらのシステム定義のレジストリ エントリの値。 ただし、Windows Vista およびそれ以降のバージョンでこれらのプロパティにアクセスするのにプロパティのキーを使用する必要があります。

システム定義のデバイス セットアップ クラスのプロパティの一覧は、次を参照してください。[デバイス セットアップ クラス プロパティことはできませんがある対応する SPCRP_Xxx 識別子](https://docs.microsoft.com/previous-versions/ff542250(v=vs.85))します。 デバイス セットアップ クラスのプロパティは、Windows Vista およびそれ以降のバージョンのプロパティへのアクセスに使用するプロパティのキー識別子が表示されます。 プロパティのキーで提供される情報には、Windows Server 2003、Windows XP、および Windows 2000 のプロパティへのアクセスに使用できる対応するレジストリ エントリの値も含まれています。

プロパティのキーを使用して、Windows Vista およびそれ以降のバージョンのデバイス セットアップ クラスのプロパティにアクセスする方法については、次を参照してください。[にアクセスするデバイス クラスのプロパティ (Windows Vista 以降)](accessing-device-class-properties--windows-vista-and-later-.md)します。

Windows Server 2003、Windows XP、および Windows 2000 でこれらのプロパティにアクセスするには、クラスのレジストリ キーを開き、これらのプロパティに対応するレジストリ エントリの値にアクセスする Windows レジストリの関数を使用します。

デバイス セットアップ クラスに対するクラスのレジストリ キーを識別するハンドルを取得する、 [ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)関数を次のパラメーター値を指定します。

-   設定*ClassGuid*要求クラスのレジストリ キーのデバイス セットアップ クラスを識別する GUID へのポインター。

-   設定*samDesired*必要なアクセス権限を示す REGSAM に型指定された値にします。

-   設定*フラグ*DIOCR_INSTALLER にします。

-   設定*MachineName*要求クラスのレジストリ キーを開くときにコンピューターの名前を含む NULL で終わる文字列へのポインター。 コンピューターがローカル コンピューターの場合は、設定*MachineName*に**NULL**します。

-   設定*予約*に**NULL**します。

この呼び出し場合[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)成功すると、 **SetupDiOpenClassRegKeyEx**要求ハンドルを返します。 関数呼び出しが失敗した場合、 **SetupDiOpenClassRegKeyEx** INVALID_HANDLE_VALUE とへの呼び出しを返します[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

クラスのレジストリ キーを識別するハンドルを取得した後に指定の呼び出しでハンドル[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)と[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)を取得またはデバイスのセットアップに対応するレジストリ エントリの値を設定するにはクラスのプロパティです。

呼び出す、 [RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)キーへのアクセスは必要なくなりました後に、クラスのレジストリ キーを閉じます。

 

 





