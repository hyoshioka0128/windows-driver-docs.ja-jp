---
title: ミニドライバーの登録
description: ミニドライバーの登録
ms.assetid: 332FEBD6-9803-4502-8F84-9DB2F17BB19B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3df83902740e4143861243de30ef4a11a91764c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553389"
---
# <a name="minidriver-registration"></a>ミニドライバーの登録


## <a name="span-iddllmainspanspan-iddllmainspanspan-iddllmainspandllmain"></a><span id="DllMain"></span><span id="dllmain"></span><span id="DLLMAIN"></span>DllMain


スマート カード ミニドライバーを実装し、エクスポート、 [ *DllMain* ](https://msdn.microsoft.com/library/windows/desktop/ms682583)をロード/アンロードを処理し、アタッチ/デタッチの通知を作成することです。 ミニドライバーの状態を管理する DLL は、このリソース割り当てられます。 実装の詳細については、次を参照してください。、 *DllMain*リファレンス トピック。

## <a name="span-iddllregisterserveranddllunregisterserverspanspan-iddllregisterserveranddllunregisterserverspanspan-iddllregisterserveranddllunregisterserverspandllregisterserver-and-dllunregisterserver"></a><span id="DllRegisterServer_and_DllUnregisterServer"></span><span id="dllregisterserver_and_dllunregisterserver"></span><span id="DLLREGISTERSERVER_AND_DLLUNREGISTERSERVER"></span>DllRegisterServer と DllUnregisterServer


*DllRegisterServer*と*DllUnregisterServer* v5 のスマート カード ミニドライバーの仕様を示す呼び出されるできなくします。 カードのミニドライバーの登録は、システム レジストリに INF ベースの更新によって行われます。

## <a name="span-idregistrationmechanismsspanspan-idregistrationmechanismsspanspan-idregistrationmechanismsspan-registration-mechanisms"></a><span id="_Registration_Mechanisms"></span><span id="_registration_mechanisms"></span><span id="_REGISTRATION_MECHANISMS"></span> 登録メカニズム


INF ベースのアプローチは、スマート カード ミニドライバーの登録に使用する必要があります。 ドライバー パッケージから適切なディレクトリにファイルのコピーと、必要なレジストリ エントリの作成、INF ファイルを使用できます。

スマート カード INF ファイルの例は、[スマート カードのプラグ アンド プレイ](smart-card-plug-and-play.md)を参照してください。

## <a name="span-idinffilerequirementsspanspan-idinffilerequirementsspanspan-idinffilerequirementsspaninf-file-requirements"></a><span id="INF_File_Requirements"></span><span id="inf_file_requirements"></span><span id="INF_FILE_REQUIREMENTS"></span>INF ファイルの要件


スマート カード INF ファイルには、各カードについては、次のレジストリ エントリを作成するディレクティブを含める必要があります。

``` syntax
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\Calais\SmartCards\VENDORCARDNAME]
"80000001"="VENDOR.dll"
"ATR"=hex:01,23,45,67,89,01,23,45,67,89,01,23,45,67,89,01,23,45
"ATRMask"=hex:ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff,ff
```

ミニドライバーは、CAPI での読み込みをサポートする場合は、レジストリ ファイルに次の行を含めます。

``` syntax
"Crypto Provider"="Microsoft Base Smart Card Crypto Provider"
```

ミニドライバーは、CNG での読み込みをサポートする場合、次の行がレジストリ ファイルに含める必要があります。

``` syntax
"Smart Card Key Storage Provider"="Microsoft Smart Card Key Storage Provider"
```

 

 





