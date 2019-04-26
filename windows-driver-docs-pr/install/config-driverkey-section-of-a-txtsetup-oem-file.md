---
title: TxtSetup.oem ファイルの Config.DriverKey セクション
description: Config.DriverKey セクションでは、特定のコンポーネントのオプションのレジストリで設定する値を指定します。
ms.assetid: 0b9fe0ff-2b97-416e-8ced-62b59eabf94a
keywords:
- Config.DriverKey セクションの TxtSetup.oem ファイルのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- Config.DriverKey Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf88e4b0b1fe90c0d951b7f1a4f4bff37dc3ce12
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353846"
---
# <a name="configdriverkey-section-of-a-txtsetupoem-file"></a>TxtSetup.oem ファイルの Config.DriverKey セクション


A **Config** 。<em>DriverKey</em>セクションでは、特定のコンポーネントのオプションのレジストリで設定する値を指定します。 Windows に必要な値を自動的に作成する、**サービス\\**<em>DriverKey</em>キー。 このセクションを使用して、追加のキーの下に作成する**サービス\\**<em>DriverKey</em>下に値と**サービス\\** <em>DriverKey</em>と**サービス\\**<em>DriverKey</em>\\*subkey_name*します。

``` syntax
[Config.DriverKey]
value = subkey_name,value_name,value_type,value
...
```

<a href="" id="subkey-name"></a>*subkey_name*  
キーの名前を指定します、**サービス\\**<em>DriverKey</em>ツリー Windows が指定した値を配置します。 存在しない場合、Windows は、キーを作成します。

場合*subkey_name*空の文字列 ("")、値がの下に配置、**サービス\\**<em>DriverKey</em>します。

*Subkey_name*などのサブキーを 1 つ以上のレベルを指定できます"subkey1\\subkey2\\subkey3"。

<a href="" id="value-name"></a>*値名*  
設定する値の名前を指定します。

<a href="" id="value-type"></a>*value_type*  
レジストリ エントリの種類を指定します。 *Value_type*次のいずれかを指定できます。

<a href="" id="reg-dword"></a>REG_DWORD  
1 つ*値*; 許可が含む最大 8 つの 16 進文字列にする必要があります。

次に、例を示します。

``` syntax
value = parameters,NumberOfButtons,REG_DWORD,2
```

<a href="" id="reg-sz-or-reg-expand-sz"></a>REG_SZ または[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)  
1 つ*値*; 許可されて格納される null で終わる文字列として解釈されます。

例:

``` syntax
value = parameters,Description,REG_SZ,"This is a text string"
```

<a href="" id="reg-binary"></a>REG_BINARY  
1 つ*値*は許可されている; が 16 進の数字の文字列を各ペアは、バイトの値として解釈されます。

たとえば (格納バイト ストリーム 00,34、ec 4 d、04、5 a)。

``` syntax
value = parameters,Data,REG_BINARY,0034eC4D045a
```

<a href="" id="reg-multi-sz"></a>REG_MULTI_SZ  
複数*値*引数を指定することは、それぞれは、コンポーネントのレジストリ文字列として解釈されます。

例:

``` syntax
value = parameters,Strings,REG_MULTI_SZ,String1,"String 2",string3
```

<a href="" id="value"></a>*値*  
値を指定しますその形式に依存*value_type*します。

次の例は、 **Config** 。<em>DriverKey</em>セクション。

``` syntax
; ...
[Config.OEMSCSI]
value = parameters\PnpInterface,5,REG_DWORD,1
; ...
```

 

 





