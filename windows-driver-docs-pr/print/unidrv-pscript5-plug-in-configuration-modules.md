---
title: Unidrv/PScript5 プラグイン構成モジュール
description: Unidrv/PScript5 プラグイン構成モジュール
ms.assetid: 806175ba-18a9-48f3-8f50-06e794d1f304
keywords:
- バージョン 3 XPS ドライバー WDK XPSDrv、Unidrv プラグイン
- バージョン 3 XPS ドライバー WDK XPSDrv、PScript5 プラグイン
- IPrintCoreHelper
- 印刷 Pscript WDK、XPSDrv プリンター ドライバー
- Unidrv、XPSDrv プリンター ドライバー
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba06c8719462c3e5c5972c8473c5d65c82efcdca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385958"
---
# <a name="unidrvpscript5-plug-in-configuration-modules"></a>Unidrv/PScript5 プラグイン構成モジュール


XPSDrv プリンター ドライバーの構成のモジュールには、Windows Vista で Unidrv または PScript5 の構成プラグインを使用してでは、次の新しい機能をサポートします。

-   PrintTicket と PrintCapabilities 機能

-   [IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelper) Unidrv と PScript5 の設定を操作するためのインターフェイス

-   XPSDrv ドキュメント イベント

-   通信の印刷フィルター パイプライン内のドライバーのフィルター

### <a name="printticket-and-printcapabilities-interface-support"></a>PrintTicket と PrintCapabilities インターフェイスのサポート

Unidrv および PScript5 の印刷ドライバー プラグインを実装、 [IPrintOemPrintTicketProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintoemprintticketprovider) PrintTicket と PrintCapabilities データをカスタマイズするインターフェイス。 このインターフェイスでメソッドを使用するプラグイン PrintTicket と PrintCapabilities プラグインでは、カスタムの機能の処理をカスタマイズします。

Unidrv と PScript5 印刷ドライバーの実装、 [IPrintTicketProvider](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554375(v=vs.85))インターフェイスし、PrintTicket と PrintCapabilities GPD または PPD ファイルに基づいているデータの初期のバージョンを生成します。 初期の処理後 Unidrv または PScript5 印刷ドライバーを呼び出して、プラグインの**IPrintOemPrintTicketProvider**インターフェイスように、プラグインは印刷ドライバーが、呼び出し元に返す前に、このデータを変更アプリケーション。

### <a name="iprintcorehelper-interface"></a>IPrintCoreHelper インターフェイス

**IPrintCoreHelper**インターフェイスにより、プラグインの印刷ドライバーの構成。

-   取得し、その Unidrv と PScript5 印刷ドライバーを使用して、DEVMODE 構造体のプライベート部分に値を設定します。

-   プリンター ドライバーの機能、オプション、および制約を列挙します。

-   完全な GPD または PPD ファイル コンテンツの一部にアクセスします。

プラグインを適切に Unidrv または PScript5 構成を設定し、完全なユーザー インターフェイス (UI) の置換機能を有効にする唯一の方法は、次を使用して、 **IPrintCoreHelper**インターフェイス。

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

次の 2 つ追加インターフェイス[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)と[IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)から派生、 **IPrintCoreHelper**インターフェイス。 これらのインターフェイスは Unidrv に固有であり、PScript5 印刷ドライバーをそれぞれ、およびドライバーごとに固有の他のメソッドが含まれます。

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

次のコード例を使用する方法を示しています、 **IPrintCoreHelper** DEVMODE 構造体からの情報を照会するインターフェイス。 この例では、XPSDrv プリンター ドライバーのサンプル コードで Windows Driver Kit (WDK) の一部です。

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

 

 




