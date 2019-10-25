---
title: Unidrv/PScript5 プラグイン構成モジュール
description: Unidrv/PScript5 プラグイン構成モジュール
ms.assetid: 806175ba-18a9-48f3-8f50-06e794d1f304
keywords:
- バージョン 3 XPS ドライバー WDK XPSDrv、Unidrv プラグイン
- バージョン 3 XPS ドライバー WDK XPSDrv、PScript5 プラグイン
- IPrintCoreHelper
- Pscript WDK print、XPSDrv 印刷ドライバー
- Unidrv、XPSDrv 印刷ドライバー
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7723a7674408a1aaece1c8211208c8b030d991c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843622"
---
# <a name="unidrvpscript5-plug-in-configuration-modules"></a>Unidrv/PScript5 プラグイン構成モジュール


Windows Vista で Unidrv または PScript5 構成プラグインを使用する XPSDrv print driver 構成モジュールは、次の新機能をサポートしています。

-   PrintTicket と PrintCapabilities の機能

-   Unidrv と PScript5 の設定を操作するための[Iprintcorehelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)インターフェイス

-   XPSDrv ドキュメントイベント

-   フィルターパイプラインでの印刷ドライバーフィルターとの通信

### <a name="printticket-and-printcapabilities-interface-support"></a>PrintTicket と PrintCapabilities インターフェイスのサポート

Unidrv および PScript5 印刷ドライバープラグインは、 [IPrintOemPrintTicketProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintoemprintticketprovider)インターフェイスを実装して、PrintTicket と PrintCapabilities データをカスタマイズします。 このインターフェイスのメソッドを使用すると、プラグインは、プラグインによって提供されるカスタム機能の PrintTicket および PrintCapabilities 処理をカスタマイズできます。

Unidrv および PScript5 印刷ドライバーは、 [IPrintTicketProvider](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))インターフェイスを実装し、GPD または PPD ファイルに基づく PrintTicket および PrintCapabilities データの初期バージョンを生成します。 最初の処理の後、Unidrv または PScript5 print driver はプラグインの**IPrintOemPrintTicketProvider**インターフェイスを呼び出します。これにより、プラグインは、このデータを変更してから呼び出し元のアプリケーションに返すようになります。

### <a name="iprintcorehelper-interface"></a>IPrintCoreHelper インターフェイス

**Iprintcorehelper**インターフェイスを使用すると、次のような印刷ドライバー構成プラグインが有効になります。

-   Unidrv および PScript5 印刷ドライバーが使用する DEVMODE 構造体のプライベート部分の値を取得および設定します。

-   印刷ドライバーの機能、オプション、および制約を列挙します。

-   GPD または部分的な PPD ファイルの内容にアクセスします。

プラグインが Unidrv または PScript5 構成を適切に設定し、完全なユーザーインターフェイス (UI) 置換機能を有効にするには、次の**Iprintcorehelper**インターフェイスを使用する方法しかありません。

```cpp
DECLARE_INTERFACE_(IPrintCoreHelper, IUnknown) {
  // IUnknown methods skipped
  STDMETHOD(CreateInstanceOfMSXMLObject)(...)
  STDMETHOD(EnumConstrainedOptions)(...)
  STDMETHOD(EnumFeatures)(...)
  STDMETHOD(EnumOptions)(...)
  STDMETHOD(GetOption)(...)
  STDMETHOD(SetOptions)(...)
  STDMETHOD(WhyConstrained)(...)
};
```

次の2つの追加のインターフェイス[Iprintcoreare Peruni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)と[Iprintcoreare Perps](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)は、 **iprintcorehelper**インターフェイスから派生しています。 これらのインターフェイスは、それぞれが Unidrv および PScript5 の印刷ドライバーに固有であり、各ドライバーに固有の追加のメソッドが含まれています。

```cpp
DECLARE_INTERFACE_(IPrintCoreHelperUni, IUnknown) {
  // IUnknown methods skipped
  // IPrintCoreHelper methods skipped
  STDMETHOD(CreateDefaultGDLSnapshot)(...)
  STDMETHOD(CreateGDLSnapshot)(...)
};

DECLARE_INTERFACE_(IPrintCoreHelperPS, IUnknown) {
  // IUnknown methods skipped
  // IPrintCoreHelper methods skipped
  STDMETHOD(GetFeatureAttribute)(...)
  STDMETHOD(GetGlobalAttribute)(...)
  STDMETHOD(GetOptionAttribute)(...)
};
```

次のコード例は、 **Iprintcorehelper**インターフェイスを使用して DEVMODE 構造体の情報を照会する方法を示しています。 この例は、Windows Driver Kit (WDK) の XPSDrv print driver サンプルコードの一部です。

```cpp
HRESULT
CBookletDMPTConv::GetDrvSettingsFromDM(
    __in    PDEVMODE                         pDevmode,
            ULONG                            cbDevmode,
    __out   GPD::Binding::DrvSettings*       pDrvSettings
    )
{
  HRESULT hr = S_OK;

  for (GPD::Binding::EGPDSettings setting = 
        GPD::Binding::EGPDSettingsMin;
      setting < GPD::Binding::EGPDSettingsMax && SUCCEEDED(hr);
      setting++)
  {
    PCSTR pszOption;
    hr = m_pCoreHelper->GetOption(
      pDevmode,
      cbDevmode, 
      m_featureNames[setting], 
      &pszOption)
    if (SUCCEEDED(hr))
    {
      hr = GPDSettingFromOptionString(
      pszOption, 
      setting, 
      pDrvSettings);
    }
  }

  return hr;
}
```

 

 




