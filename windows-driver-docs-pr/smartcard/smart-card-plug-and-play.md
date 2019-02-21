---
title: スマート カードのプラグ アンド プレイ
description: スマート カードのプラグ アンド プレイ
ms.assetid: AE65A450-62A4-4774-A935-B7CB4301CCF4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f2e345399fd9a7b0e885b2bb3bf7979198543d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528819"
---
# <a name="smart-card-plug-and-play"></a>スマート カードのプラグ アンド プレイ


## <a name="span-idpairingprocessspanspan-idpairingprocessspanspan-idpairingprocessspan-pairing-process"></a><span id="_Pairing_Process"></span><span id="_pairing_process"></span><span id="_PAIRING_PROCESS"></span> ペアリング プロセス


オペレーティング システムには、次の手順を既にインストールされているミニドライバーのスマート カードのペアリングが次に示します。

-   スマート カードの ATR を取得します。
-   HKEY 内のエントリを反復処理\_ローカル\_マシン\\ソフトウェア\\Microsoft\\暗号化\\Calais\\スマート カードのレジストリ キーし、次の操作を行います。

    -   スマート カードから取得された ATR をレジストリに格納されている ATRMask サブキーの値を適用します。
    -   マスクされた ATR 値をレジストリに格納されている ATR サブキーの値と比較します。
    -   ATR の 2 つの値が一致している場合は、処理を停止し、スマート カードと対応するミニドライバーをペアリングします。

スマート カード ATR と ATRMask 値は、スマート カードのミニドライバーの誤ったペアリングを回避するために慎重に選択する必要があります。 レジストリに格納されているスマート カードの ATR 値は、スマート カードから読み取った ATR、ATRMask が適用された後に、予期される値にすることがあります。 それ以外の場合、カードと、レジストリからマスクされた ATR 値が一致しないし、失敗、ペアリングします。

初めての Windows Update サイトで、適切なミニドライバーの検索結果をカード リーダー トリガー プラグ アンド プレイ イベントにスマート カードが挿入されますを以降、Windows 7 にします。 Windows Update でドライバーを検索する Windows を生成するデバイス ID は、次の要因によって異なります。

-   ATR から履歴のバイト数。 ATR の履歴 (バイト) の詳細については、標準の ISO/IEC 7816-4:2005(E) の第 8 章を参照してください。
-   タグ 0x7F68 で GUID の一覧を Microsoft プラグ アンド プレイの補助アプリケーションの存在します。
-   受信トレイのドライバーとペアになるをカード上の PIV アプリケーションの存在します。
-   Microsoft 汎用プロファイルに受信トレイのドライバーとペアになるをカード上の GID (ジェネリック ユーザー デバイスの仕様) アプリケーションの存在します。

詳細についてはプラグ アンド プレイし、Winscard のスマート カードの検出プロセスを参照してください。[スマート カードの検出プロセス](discovery-process.md)します。 これらのプロセスは、スマート カードの一意のデバイス ID の生成の結果します。

**注**  スマート カード用に Windows が生成するデバイス ID を調べるに推奨されるアプローチは、Windows 7 または Windows の以降のバージョンを実行しているコンピューターに接続されているスマート カード リーダーにスマート カードを挿入します。 デバイス ID は、デバイス マネージャーでのスマート カード デバイスの [ハードウェア Id] プロパティを調べることで確認できます。

 

## <a name="span-idsampleinfforx86andamd64spanspan-idsampleinfforx86andamd64spanspan-idsampleinfforx86andamd64spansample-inf-for-x86-and-amd64"></a><span id="Sample_INF_for_x86_and_amd64"></span><span id="sample_inf_for_x86_and_amd64"></span><span id="SAMPLE_INF_FOR_X86_AND_AMD64"></span>X86 および amd64 サンプル INF


次にスマート カードのインストールでは、Windows 8 および Windows の以前のバージョンの INF ファイルの例を示します。 この INF ファイルは、X86 および AMD64 CPU プラットフォームでのインストールに修飾されます。

**注**  展開に関する問題を避けるため、強くお勧め Winqual するドライバー パッケージを送信する前にすべての対象となるオペレーティング システムのクリーン インストールで、ドライバー パッケージをテストします。

 

``` syntax
;
;FabrikamVendor Smartcard Minidriver for an x86 and x64 based package.
;

[Version]
Signature="$Windows NT$"
Class=SmartCard
ClassGuid={990A2BD7-E738-46c7-B26F-1CF8FB9F1391}
Provider=%FABRIKAMVENDOR%
CatalogFile=delta.cat
DriverVer=10/03/2008,7.0.0.4

[Manufacturer]
%FABRIKAMVENDOR%=FabrikamVendor,NTamd64,NTamd64.6.1,NTx86,NTx86.6.1

[FabrikamVendor.NTamd64]
%FabrikamCardDeviceName%=FabrikamVendor64_Install,SCFILTER\CID_51FF0800

[FabrikamVendor.NTx86]
%FabrikamCardDeviceName%=FabrikamVendor32_Install,SCFILTER\CID_51FF0800

[FabrikamVendor.NTamd64.6.1]
%FabrikamCardDeviceName%=FabrikamVendor64_61_Install,SCFILTER\CID_51FF0800

[FabrikamVendor.NTx86.6.1]
%FabrikamCardDeviceName%=FabrikamVendor32_61_Install,SCFILTER\CID_51FF0800

[DefaultInstall]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[DefaultInstall.ntamd64]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault

[DefaultInstall.NTx86]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[SourceDisksFiles]
Fabrikamcm64.dll=1
Fabrikamcm.dll=1

[SourceDisksNames]
1 = %MediaDescription%

[FabrikamVendor64_Install.NT]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault

[FabrikamVendor64_61_Install.NT]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[FabrikamVendor32_Install.NT]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[FabrikamVendor32_61_Install.NT]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[FabrikamVendor64_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services

[FabrikamVendor32_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services


[FabrikamVendor64_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[FabrikamVendor64_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[FabrikamVendor64_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[FabrikamVendor32_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[FabrikamVendor32_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[FabrikamVendor32_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[amd64_CopyFiles]
Fabrikamcm.dll,Fabrikamcm64.dll

[x86_CopyFiles]
Fabrikamcm.dll

[wow64_CopyFiles]
Fabrikamcm.dll

[AddRegWOW64]
HKLM, %SmartCardNameWOW64%,"ATR",0x00000001,3b,04,51,ff,08,00
HKLM, %SmartCardNameWOW64%,"ATRMask",0x00000001,ff,ff,ff,ff,ff,ff
HKLM, %SmartCardNameWOW64%,"Crypto Provider",0x00000000,"Microsoft Base Smart Card Crypto Provider"
HKLM, %SmartCardNameWOW64%,"Smart Card Key Storage Provider",0x00000000,"Microsoft Smart Card Key Storage Provider"
HKLM, %SmartCardNameWOW64%,"80000001",0x00000000,%SmartCardCardModule%

[AddRegDefault]
HKLM, %SmartCardName%,"ATR",0x00000001,3b,04,51,ff,08,00
HKLM, %SmartCardName%,"ATRMask",0x00000001,ff,ff,ff,ff,ff,ff
HKLM, %SmartCardName%,"Crypto Provider",0x00000000,"Microsoft Base Smart Card Crypto Provider"
HKLM, %SmartCardName%,"Smart Card Key Storage Provider",0x00000000,"Microsoft Smart Card Key Storage Provider"
HKLM, %SmartCardName%,"80000001",0x00000000,%SmartCardCardModule%

[DestinationDirs]
amd64_CopyFiles=10,system32
x86_CopyFiles=10,system32
wow64_CopyFiles=10,syswow64


; =================== Generic ==================================

[Strings]
FABRIKAMVENDOR ="FabrikamVendor"
MediaDescription="FabrikamVendor Smart Card Minidriver Installation Disk"
FabrikamCardDeviceName="FabrikamVendor Minidriver for Smart Card"
SmartCardName="SOFTWARE\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardNameWOW64="SOFTWARE\Wow6432Node\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardCardModule="Fabrikamcm.dll"
```

次に、この種類の INF ファイルに必要です。

-   デバイスの ATR 履歴バイトまたはデバイスのスマート カード フレームワークの識別子のデコードされた値にする必要があります %fabrikamcarddevicename% 文字列によって指定されているハードウェア ID。 この識別子の詳細については、スマート カードの検出プロセスの「Windows スマート カードのフレームワークのカード識別子」セクションを参照してください。
-   DefaultInstall セクションは、スマート カード ミニドライバーのパッケージの INF ファイルでは必須です。

 

 





