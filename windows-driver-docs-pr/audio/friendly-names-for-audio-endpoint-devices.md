---
title: オーディオ エンドポイント デバイスのフレンドリ名
description: オーディオ エンドポイント デバイスのフレンドリ名
ms.assetid: e0937d20-dd5b-453f-99f6-4e501f0f0e5b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52fad97a1ada2d3c07f58f67616dcf2d64dfc61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571751"
---
# <a name="friendly-names-for-audio-endpoint-devices"></a>オーディオ エンドポイント デバイスのフレンドリ名


Windows Vista、Windows Server 2008 以降のバージョンの Windows では、オーディオのサブシステムは、エンドポイントのオーディオ デバイス、スピーカー、ヘッドホン、マイク、および CD プレーヤーの概念をサポートします。 このオーディオ エンドポイントの概念により、ユーザーが直接操作するエンドポイント デバイスを参照しているユーザー インターフェイスを持つユーザー フレンドリなオーディオ アプリケーションを作成します。 これらのエンドポイントでは、「スピーカー」、「ヘッドホン」、「マイク」、「CD プレーヤー」アプリケーションは、そのユーザー インターフェイスで表示できるなどのフレンドリ名があります。 エンドポイント デバイスの詳細については、[オーディオ エンドポイント デバイス](https://go.microsoft.com/fwlink/p/?linkid=130876)を参照してください。

オーディオのサブシステムは、KS フィルターとして、オーディオのアダプターでプラグ アンド プレイ (PnP) デバイスをモデル化します。 データ ストリーム入力し、KS ピンを使用して、フィルターを終了します。 ブリッジの暗証番号 (pin) は、KS フィルターににより、エンドポイントのオーディオ デバイスが接続する KS pin です。 ブリッジの pin の詳細については、[オーディオ フィルター グラフ](audio-filter-graphs.md)を参照してください。

オーディオのサブシステムは、エンドポイント デバイスに接続するブリッジの暗証番号 (pin) のプロパティを調べることによって、エンドポイントのオーディオ デバイスに関する情報を取得します。 このような 1 つのプロパティが、 [category プロパティをピン留め](pin-category-property.md)([**KSPROPERTY\_PIN\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff565192))。 

アダプターのドライバーがのテーブルを提供する各 KS フィルター [ **PCPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537721) KS ピンのプロパティをフィルターを記述する構造体。 暗証番号 (pin) カテゴリに GUID が格納されている、 **KsPinDescriptor.Category** 、PCPIN のメンバー\_記述子構造体。 ブリッジ暗証番号 (pin) の暗証番号 (pin) カテゴリの値の GUID を示しますブリッジの暗証番号 (pin) に接続するエンドポイントの種類。 暗証番号 (pin) カテゴリの GUID KSNODETYPE など\_マイクは、ブリッジの暗証番号 (pin) が、マイク、GUID KSNODETYPE に接続することを示します\_スピーカーでは、ブリッジの暗証番号 (pin) がスピーカー、という具合に接続することを示します。 KSNODETYPE\_*XXX* Guid が Ksmedia.h ヘッダー ファイルで定義されます。

さらに、 **PCPIN\_記述子**一意の名前によって、暗証番号 (pin) を識別するために使用できる GUID が含まれています。  この暗証番号 (pin) の名前に GUID が格納されている、 **KsPinDescriptor.Name** 、PCPIN のメンバー\_記述子構造体。 この名前を使用する GUID が、([**KSPROPERTY\_PIN\_名前**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-name))、pin でレジストリにフレンドリ名を関連付けるプロパティが見つかりました。 

オーディオのサブシステムを呼び出す、 **KSPROPERTY\_PIN\_名前**にフレンドリ名をオーディオのエンドポイントに関連付けるプロパティ。 KS レジストリの説明で unicode 文字列の最初に検索してこの要求を処理する、 **KsPinDescriptor.Name** GUID。  KS にエントリが見つからない場合、レジストリを記述する unicode 文字列を検索、 **KsPinDescriptor.Category** GUID。  

以降で**Windows 10 REDSTONE 5** KS がデバイスのソフトウェアのキー内のエントリを最初に、レジストリを検索するときにします。  これは、デバイス ドライバーの INF の [モデル] セクションで参照されている、AddReg セクションで INF によって作成されます。  AddReg セクションは、HKR を使用してこれらのエントリを構築します\\MediaCategories キー。 これにより、GUID がデバイスに一意かどうか、ドライバー開発者は、デバイスに固有のフレンドリ名の名前とカテゴリの Guid の両方を作成できます。

デバイスのソフトウェアのキーのエントリがインストールされていないか、ドライバーがより前のバージョンのオペレーティング システムで実行されている**Windows 10 REDSTONE 5**、KS では HKLM\\システム\\CurrentControlSet\\コントロール\\MediaCategories レジストリ キー。 この 2 番目のキーは、グローバル名前空間として扱われます。  以降で**Windows 10 REDSTONE 5**この領域は、グローバル定義の予約されており、新しいドライバーでは変更しないでください。  このキーのエントリの変更は将来の OS ではサポートされないリリースします。

標準的なカテゴリの Guid のピンを公開するオーディオ デバイスは、含める必要があります/受信トレイ KS 必要があります。INF または KSCAPTUR します。デバイス INF の INF 名前登録します。  これらの受信トレイには Inf には、ドライバーに設定することがありますが事前定義済みのカテゴリの Guid の既定のフレンドリ名の定義が含まれます。 これらは、同じ Guid で見つかった、 **KsPinDescriptor.Category** 、PCPIN のメンバー\_記述子構造体。 カテゴリの GUID KSNODETYPE など\_マイク エントリが関連付けられているフレンドリ名「マイク」とカテゴリ GUID KSNODETYPE\_スピーカー エントリが「スピーカー」の名前を指定し、関連付けられているフレンドリ。

Guid と両方のカテゴリの表示名と名前の Guid が、HKR の下に格納されている\\HKLM のグローバル定義の中に MediaCategories\\システム\\CurrentControlSet\\コントロール\\MediaCategories パス。 レジストリで、各 GUID 名はペアには、GUID 文字列が MediaCategories キーの下のサブ キーとして使用されます。  GUID キー フレンドリ名を Unicode の下には、"Name"変数の下の値を文字列します。 

フレンドリ名とオーディオのサブシステムによって適切に定義されている pin のカテゴリの [なし] には、デバイスについて説明する場合、は、独自の pin のカテゴリおよび名前の Guid と、INF でそれらをわかりやすい名前を関連付けます。 暗証番号 (pin) カテゴリの GUID が一意であることを確認するのにには、GUID を生成するのに Uuidgen.exe などのユーティリティを使用します。 次に、レジストリ パス HKR にピン留めするカテゴリの GUID とフレンドリ名を書き込むオーディオ アダプターをインストールする INF ファイルを変更\\MediaCategories します。 次のコード例では、2 つのピン留めするカテゴリの Guid と、関連付けられているフレンドリ名をレジストリに追加する INF ファイルのフラグメントを示します。

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

両方の GUID の文字列は、Uuidgen.exe によって生成されました。

アプリケーションは、デバイスを使用して、エンドポイントのオーディオ デバイスのプロパティにアクセスできます**IPropertyStore**インターフェイス。 インターフェイスは、Functiondiscoverykeys で定義されているプロパティのキーを使用して\_devpkey.h とプロパティを識別するために Mmdeviceapi.h ヘッダー ファイル。 アプリケーションで使用できます、**鍵\_デバイス\_FriendlyName**エンドポイント デバイスのフレンドリ名を取得するプロパティのキー。 使用して領域の制約があるユーザー インターフェイスでは、フレンドリ名の短いバージョンを取得できる、**鍵\_デバイス\_DeviceDesc**プロパティのキー。 これらのプロパティのキーの詳細については、[IMMDevice::OpenPropertyStore](https://go.microsoft.com/fwlink/p/?linkid=155067)を参照してください。

**IPropertyStore**インターフェイス インスタンスが、エンドポイントのオーディオ デバイス向けの永続的なプロパティ ストアを保持します。 プロパティ ストアをその初期値をコピーする、**鍵\_デバイス\_DeviceDesc**プロパティのキーを HKLMのレジストリパスにKS暗証番号(pin)カテゴリのGUIDに関連付けられているフレンドリ名の文字列から\\システム\\CurrentControlSet\\コントロール\\MediaCategories します。 アプリケーションが読み取ることができます、**鍵\_デバイス\_DeviceDesc**プロパティ ストアからプロパティ値 (名文字列) が、値は変更できません。 ただし、ユーザーは、Windows のマルチ メディア コントロール パネル、Mmsys.cpl を使用して名前を変更することができます。 たとえば、Windows Vista では、レンダリング エンドポイント デバイスの名前を変更するのに、次の手順を使用できます。

1.  Mmsys.cpl を実行するには、コマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

    ```console
    mmsys.cpl
    ```

    (をタスク バーの右側にある通知領域のスピーカーのアイコンを右クリックして Mmsys.cpl を実行する代わりに、**再生デバイス**)。

2.  レンダリング デバイスの名前をクリックし、クリックして**プロパティ**します。

3.  [プロパティ] ウィンドウ、**全般**タブ。フレンドリ名は、プロパティ シートの上部にあるテキスト ボックスに表示されます。 フレンドリ名を編集してをクリックして変更を保存**OK**します。

上記の手順では、エンドポイントのオーディオ デバイスのプロパティ ストアに格納されているフレンドリ名を変更します。 次の手順は同じ KS 暗証番号 (pin) カテゴリに属している他のオーディオ エンドポイント デバイスに関連付けられているフレンドリ名に影響を与えるありません。 ある KS 名を直接照会しているコンポーネントへの影響はありません。
