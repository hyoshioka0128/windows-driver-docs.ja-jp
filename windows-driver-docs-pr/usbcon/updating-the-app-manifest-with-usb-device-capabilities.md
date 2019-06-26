---
Description: このトピックでは、Windows.Devices.Usb 名前空間を使用する Windows アプリを必要とされるデバイスの機能について説明します。
title: アプリ マニフェストへの USB デバイス機能の追加方法
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: c3cd0db64cf5fe520efc1fefe5d18853380f7a3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368761"
---
# <a name="how-to-add-usb-device-capabilities-to-the-app-manifest"></a>アプリ マニフェストへの USB デバイス機能の追加方法


**概要**

-   USB デバイスの機能では、Package.appxmanifest を更新する必要があります。
-   デバイス クラスには、サポートされているクラスのいずれかを指定する必要があります。

このトピックでは、使用する Windows アプリを必要とされるデバイスの機能を説明します、 [ **Windows.Devices.Usb** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)名前空間。

## <a name="usb-device-capability-usage"></a>USB デバイスの機能の使用状況


USB アプリは、特定のデバイスの機能を含める必要があります、[アプリ パッケージのマニフェスト](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)デバイスに関する重要な情報を指定します。 階層の順序で、必要な要素を示します。

[ **&lt;DeviceCapability&gt;** ](https://docs.microsoft.com/uwp/schemas/appxpackage/appxmanifestschema/element-devicecapability):**名前**属性は"usb"である必要があります。

**&lt;デバイス&gt;** :**Id**属性は、ベンダーと製品 Id を指定する必要がありますまたは"any"関数の型と一致する任意のデバイスにアクセスできるようにすることができます。

**&lt;関数&gt;** :**型**属性は、デバイス クラスのコードや名前など、デバイス インターフェイスの GUID を指定できます。

**注**  Microsoft Visual Studio 2013 での USB デバイスの機能を変更することはできません。 Package.appxmanifest ファイルを右クリックする必要があります**ソリューション エクスプ ローラー**選択**プログラムから開く.** 、し**XML (テキスト) エディター**します。 プレーンな XML では、ファイルが開きます。

 

```XML
<DeviceCapability Name="usb">
    <Device Id="vidpid:xxxx xxxx">
      <Function Type="classId:xx xx xx"/>
      <Function Type="name:xxxxx"/>
      <Function Type="winUsbId:xxxxx"/>
    </Device>
</DeviceCapability>
```

## <a name="supported-usb-device-classes"></a>サポートされている USB デバイス クラス


-   名前と、サポートされているデバイス クラスのコードの値は次のとおりです。

    -   `name:cdcControl,           classId:02 * *`
    -   `name:physical, classId:05 * *`
    -   `name:personalHealthcare,   classId:0f 00 00`
    -   `name:activeSync,           classId:ef 01 01`
    -   `name:palmSync,             classId:ef 01 02`
    -   `name:deviceFirmwareUpdate, classId:fe 01 01`
    -   `name:irda,                 classId:fe 02 00     `
    -   `name:measurement,          classId:fe 03 *`
    -   `name:vendorSpecific,       classId:ff * *`

    **注**  DeviceFirmwareUpdate クラスに属するデバイスは、その PC で OEM によって明示的に宣言されている特権のあるアプリのみがアクセスできます。

     

-   これらは、不明なインターフェイスであるために、これらのクラス コードのベンダーと製品 id を指定する、アプリが必要です。

    -   CDC (0X02)
    -   CDC データ (0x0A)
    -   その他 (0xEF)
    -   特定のアプリケーション (0 xfe)
    -   ベンダー固有 (0 xff)
-   これらの USB デバイス クラスがサポートされていません。

    -   無効なクラス (0x00)
    -   オーディオ クラス (0x01)
    -   HID class(0x03)
    -   Image クラス (0x06)
    -   プリンター クラス (0x07)
    -   大容量記憶装置クラス (0x08)
    -   スマート カード クラス (0x0B)
    -   オーディオ/ビデオ クラス (0x10)
    -   (など、ワイヤレス USB ホスト/ハブ) のコント ローラーを (0xE0) ワイヤレスします。

## <a name="usb-device-capability-example"></a>USB デバイスの機能の例


USB デバイスの機能を定義するためのいくつかの例を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>例</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id="any"&gt;
    &lt;Function Type="classId:ef 01 01"/&gt;
    &lt;Function Type="name:stillImage"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>任意のデバイスの ActiveSync または StillImage インターフェイスにアクセスするアプリを許可します。 アプリは、これらは既知のクラス型であるために、ベンダーや製品識別子を指定する必要はありません。</p></td>
</tr>
<tr class="even">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id="vidpid:045e 930a"&gt;
    &lt;Function Type="name:vendorSpecific"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>OSR USB Fx2 デバイスのベンダー固有のインターフェイスにアクセスするアプリを許可します。</p></td>
</tr>
<tr class="odd">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id="vidpid:045e 930a"&gt;
    &lt;Function Type="classId:ff * <em>"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>OSR USB Fx2 デバイスの異なるバージョンのベンダー固有のインターフェイスにアクセスするアプリを許可します。 ClassId 形式に注意してください:"ff * *"。 クラスのコードは、"ff"の後に、ワイルドカード (</em>) とプロトコルのサブクラス コードを含めます。</p></td>
</tr>
<tr class="even">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id=" vidpid:1234 5678"&gt;
    &lt;Function Type="winUsbId:"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>MS OS 記述子またはデバイスの INF に GUID が定義されているデバイスのインターフェイスを持つデバイスにアクセスするアプリを許可します。</p>
<p>この場合、デバイス Id の値では、"any"は等しくない必要があります。</p></td>
</tr>
</tbody>
</table>

 

**CustomUsbDeviceAccess サンプル用のアプリ マニフェスト パッケージ**

```xml
  <Capabilities>
      <!--When the device's classId is FF * *, there is a predefined name for the class. You can use the name instead of the class id. 
          There are also other predefined names that correspond to a classId.-->
      <m2:DeviceCapability Name="usb">
          <!--OSRFX2 Device-->
          <m2:Device Id="vidpid:0547 1002">
              <m2:Function Type="classId:ff * *"/>
              <!--<m2:Function Type="name:vendorSpecific"/>-->
          </m2:Device>
          <!--SuperMutt Device-->
          <m2:Device Id="vidpid:045E 0611">
              <!--<m2:Function Type="classId:ff * *"/>-->
              <m2:Function Type="name:vendorSpecific"/>
          </m2b:Device>
      </m2:DeviceCapability>
  </Capabilities>
```

## <a name="related-topics"></a>関連トピック
[USB デバイス用の UWP アプリ](writing-usb-device-companion-apps-for-microsoft-store.md)  



