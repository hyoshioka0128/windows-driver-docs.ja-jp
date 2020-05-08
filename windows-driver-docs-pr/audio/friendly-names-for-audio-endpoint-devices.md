---
title: オーディオ エンドポイント デバイスのフレンドリ名
description: オーディオ エンドポイント デバイスのフレンドリ名
ms.assetid: e0937d20-dd5b-453f-99f6-4e501f0f0e5b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63e63f8dbdae0d2cb8c6303ff5010da39b322003
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925615"
---
# <a name="friendly-names-for-audio-endpoint-devices"></a>オーディオ エンドポイント デバイスのフレンドリ名


Windows Vista、Windows Server 2008、およびそれ以降のバージョンの Windows では、オーディオサブシステムは、スピーカー、ヘッドホン、マイク、CD プレーヤーなどのオーディオエンドポイントデバイスの概念をサポートしています。 このオーディオエンドポイントの概念は、ユーザーが直接操作するエンドポイントデバイスを参照するユーザーインターフェイスを持つユーザーフレンドリなオーディオアプリケーションを作成するのに役立ちます。 これらのエンドポイントには、アプリケーションがユーザーインターフェイスに表示できる "スピーカー"、"ヘッドホン"、"マイク"、"CD プレーヤー" などのわかりやすい名前が付いています。 エンドポイントデバイスの詳細については、「[オーディオエンドポイントデバイス](https://docs.microsoft.com/windows/win32/coreaudio/audio-endpoint-devices)」を参照してください。

オーディオサブシステムは、オーディオアダプター上のプラグアンドプレイ (PnP) デバイスを KS フィルターとしてモデル化します。 データストリームは、KS ピンを使用してフィルターを入力し、終了します。 ブリッジピンは、オーディオエンドポイントデバイスが KS フィルターに接続するために使用される KS pin です。 ブリッジピンの詳細については、「[オーディオフィルターグラフ](audio-filter-graphs.md)」を参照してください。

オーディオサブシステムは、エンドポイントデバイスの接続先のブリッジピンのプロパティを調べることによって、オーディオエンドポイントデバイスに関する情報を取得します。 このようなプロパティの1つは、"[ピンカテゴリ" プロパティ](pin-category-property.md)([**ksk プロパティ\_\_ピンカテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-category)) です。 

各 KS フィルターについて、アダプタードライバーは、フィルターの KS ピンのプロパティを記述する[**pcpin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)構造のテーブルを提供します。 Pin カテゴリの GUID は、PCPIN **KsPinDescriptor.Category** \_記述子構造体の KsPinDescriptor メンバーに格納されます。 ブリッジピンの場合、ピンカテゴリの GUID の値は、ブリッジピンに接続するエンドポイントの種類を示します。 たとえば、ピンカテゴリ GUID KSNODETYPE\_マイクはブリッジピンがマイクに接続していることを示し、guid KSNODETYPE\_スピーカーはブリッジピンがスピーカーに接続していることを示します。 KSNODETYPE\_*XXX* guid は、ksmedia .h ヘッダーファイルで定義されています。

さらに、 **pcpin\_記述子**には、一意の名前で pin を識別するために使用できる GUID が含まれています。  この pin 名の GUID は、PCPIN\_記述子構造体の**KsPinDescriptor.Name**メンバーに格納されます。 この名前の GUID は、([**Ksk\_プロパティの pin\_名**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-name)) プロパティによって使用され、レジストリで見つかったフレンドリ名を PIN と関連付けます。 

オーディオサブシステムは、 **Ksk プロパティ\_の\_PIN NAME**プロパティを呼び出して、フレンドリ名をオーディオエンドポイントに関連付けます。 KS は、まず、 **KsPinDescriptor.Name** GUID を記述するレジストリ内の unicode 文字列を検索することによって、この要求を処理します。  がエントリを見つけられない場合は、レジストリで**KsPinDescriptor** GUID を記述する unicode 文字列を検索します。  

**Windows 10 REDSTONE 5**以降では、レジストリを検索するときに、最初にデバイスのソフトウェアキーのエントリが検索されます。  これは、デバイスドライバーの INF の [モデル] セクションによって参照される AddReg セクションを通じて、INF によって作成されます。  AddReg セクションでは、HKR\\MediaCategories キーを使用してこれらのエントリを構築します。 これにより、ドライバーの開発者は、GUID がデバイスに対して一意であるかどうかにかかわらず、名前とカテゴリの Guid の両方に対してデバイス固有のフレンドリ名を作成できます。

デバイスのソフトウェアキーにエントリがインストールされていない場合、またはドライバーが**Windows 10 REDSTONE 5**より前のオペレーティングシステムで実行されて\\いる\\場合\\、\\KS は HKLM system CurrentControlSet Control MediaCategories レジストリキーを調べます。 この2番目のキーは、グローバルな名前空間として扱われます。  **Windows 10 REDSTONE 5**以降では、この領域はグローバル定義用に予約されており、新しいドライバーによって変更することはできません。  このキーの下にあるエントリの変更は、今後の OS リリースではサポートされません。

標準のカテゴリ Guid で pin を公開するオーディオデバイスには、受信トレイ KS が含まれている必要があります。INF または KSCAPTUR。デバイスの INF に登録されている INF 名。  これらの受信トレイの Inf には、ドライバーによって設定されることがある、事前に定義されたカテゴリ Guid の既定のフレンドリ名定義が含まれています。 これらは、PCPIN\_記述子構造体の**KsPinDescriptor**メンバーで見つかったものと同じ guid です。 たとえば、カテゴリ GUID KSNODETYPE\_マイクエントリには、関連付けられたフレンドリ名 "マイク" があり\_、category guid KSNODETYPE スピーカエントリには、関連付けられているフレンドリ名 "スピーカー" が付いています。

カテゴリと名前の両方の Guid の Guid とフレンドリ\\名は hkr MediaCategories の下に格納され\\、\\グローバル\\定義\\では HKLM SYSTEM CurrentControlSet Control MediaCategories パスが使用されます。 レジストリ内の GUID と名前のペアごとに、GUID 文字列が MediaCategories キーの下のサブキーとして使用されます。  GUID キーの下で、"Name" 変数の下に Unicode 文字列値の表示名を指定します。 

オーディオサブシステムで定義されているフレンドリ名とピンカテゴリによってデバイスが適切に記述されていない場合は、独自の pin カテゴリと名前 Guid を定義し、フレンドリ名を INF で関連付けることができます。 Pin カテゴリの GUID が一意であることを確認するには、Uuidgen.exe などのユーティリティを使用して GUID を生成します。 次に、オーディオアダプターをインストールする INF ファイルを変更して、pin カテゴリの GUID とフレンドリ名をレジストリパス HKR\\MediaCategories に書き込みます。 次のコード例は、2つのピンカテゴリ Guid とそれに関連付けられている表示名をレジストリに追加する INF ファイルのフラグメントを示しています。

```inf
[Manufacturer]
MyOEMName=Unicorn,NTamd64

[Unicorn.NTamd64]
MyDeviceName=MyDevice,Root\MyDevice

[MyDevice.NT]
Include=ks.inf, kscaptur.inf
Needs=KS.Registration, KSCAPTUR.Registration.NT
CopyFiles=MyDevice.CopyFiles
AddReg=PinNameRegistration

...

[PinNameRegistration]
HKR,%MediaCategories%\%GUID.MyNewEndpointCategory%,Name,,%Name.MyNewEndpointCategory%
HKR,%MediaCategories%\%GUID.MyNewEndpointName%,Name,,%Name.MyNewEndpointName%

...

[Strings]
MyOEMName="Unicorns Inc."
MyDeviceName="Sparkly Unicorn"
MediaCategories="MediaCategories"

GUID.MyNewEndpointCategory="{B72FBD1A-4634-4240-B207-0E6B52F3701C}"
GUID.MyNewEndpoint_2="{71DD3A5D-E303-49A0-ACEE-908634AA9520}"

Name.MyNewEndpointCategory="Unicorn"
Name.MyNewEndpointName="Fred the Unicorn"
```

両方の GUID 文字列は、Uuidgen.exe によって生成されました。

アプリケーションは、デバイスの**IPropertyStore**インターフェイスを使用して、オーディオエンドポイントデバイスのプロパティにアクセスできます。 インターフェイスは、Functiondiscoverykeys\_Devpkey および Mmdeviceapi .h ヘッダーファイルで定義されているプロパティキーを使用して、プロパティを識別します。 アプリケーションでは、 **\_PKEY デバイス\_の FriendlyName**プロパティキーを使用して、エンドポイントデバイスのフレンドリ名を取得できます。 領域を制限するユーザーインターフェイスでは、 **\_PKEY Device\_DeviceDesc**プロパティキーを使用して、より短いバージョンのフレンドリ名を取得できます。 これらのプロパティキーの詳細については、「 [IMMDevice:: OpenPropertyStore](https://docs.microsoft.com/windows/win32/api/mmdeviceapi/nf-mmdeviceapi-immdevice-openpropertystore)」を参照してください。

**IPropertyStore**インターフェイスインスタンスは、オーディオエンドポイントデバイスの永続的なプロパティストアを保持します。 プロパティストアは、レジストリパス HKLM\\SYSTEM\\\\CurrentControlSet CONTROL\\MediaCategories の KS pin カテゴリ GUID に関連付けられているフレンドリ名文字列から、 **PKEY\_Device\_DeviceDesc**プロパティキーの初期値をコピーします。 アプリケーションでは、プロパティストアから**\_PKEY Device\_DeviceDesc**プロパティ値 (名前文字列) を読み取ることができますが、値を変更することはできません。 ただし、ユーザーは Windows のマルチメディアコントロールパネルである Mmsys を使用して名前を変更できます。 たとえば、Windows Vista では、次の手順を使用して、レンダリングエンドポイントデバイスの名前を変更できます。

1.  Mmsys を実行するには、コマンドプロンプトウィンドウを開き、次のコマンドを入力します。

    ```console
    mmsys.cpl
    ```

    (または、タスクバーの右側にある通知領域のスピーカーアイコンを右クリックし、[**再生デバイス**] をクリックして、mmsys を実行できます)。

2.  レンダリングデバイスの名前をクリックし、[**プロパティ**] をクリックします。

3.  プロパティウィンドウで、[**全般**] タブをクリックします。フレンドリ名は、プロパティシートの上部にあるテキストボックスに表示されます。 フレンドリ名を編集し、[ **OK]** をクリックして変更を保存することができます。

前の手順では、オーディオエンドポイントデバイスのプロパティストアに格納されているフレンドリ名を変更します。 これらの手順は、同じ KS ピンカテゴリに属する他のオーディオエンドポイントデバイスに関連付けられたフレンドリ名には影響しません。 また、名前のために KS を直接照会する可能性のあるコンポーネントには影響しません。
