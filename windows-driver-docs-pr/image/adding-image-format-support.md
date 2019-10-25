---
title: イメージ形式のサポートの追加
description: イメージ形式のサポートの追加
ms.assetid: 1ffa7c0d-23ec-402a-a0b5-fb5596a851bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58e9caa0c81040165bf8d948c1023cacac0a993a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840912"
---
# <a name="adding-image-format-support"></a>イメージ形式のサポートの追加





WIA ミニドライバーは、 [**IWiaMiniDrv::D rvgetwiaformatinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)メソッドでイメージ形式を wia サービスに報告します。

### <a href="" id="implementing-iwiaminidrv-drvgetwiaformatinfo"></a>IWiaMiniDrv の実装::d rvGetWiaFormatInfo

WIA サービスは**IWiaMiniDrv::D rvgetwiaformatinfo**メソッドを呼び出して、wia デバイスでサポートされている TYMED と形式のペアを取得します。

Wia ドライバーは、(この wia ドライバーに格納され、この WIA ドライバーによって解放される) メモリを割り当てて、WIA\_形式\_情報構造 (Microsoft Windows SDK ドキュメントで説明) の配列を含める必要があります。 WIA ドライバーで割り当てられたメモリへのポインターを*ppwfi*に渡す必要があります。 この操作は直接行われませんが、ポインターへのポインターが使用されます。 次の例では、 *ppwfi*が m\_WIAFormatInfo\[0\]のアドレスに設定されています。これは、構造体の最初のメンバーのアドレスに評価されます。

このメモリは、WIA サービスによって解放されないことに注意してください。 この割り当てられたメモリを管理するのは、WIA ドライバーの役割です。

WIA ドライバーは、 *pcelt*パラメーターが指すメモリ位置に割り当てられている構造体の数を書き込みます。

Wia デバイスでは、WIA\_形式\_INFO 構造体の**guidFormatID**メンバーをイメージ形式の GUID に設定する必要があります。 デバイスは、この構造体の**lTymed**メンバーに、イメージ形式 GUID に関連付けられている TYMED 値を設定する必要があります。

有効な TYMED 値 ("メディアの種類" とも呼ばれます) は次のとおりです。

TYMED\_ファイル

TYMED\_マルチページ\_ファイル

TYMED\_コールバック

TYMED\_マルチページ\_コールバック

次の例は、 [**IWiaMiniDrv::D rvgetwiaformatinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)の実装を示しています。

```cpp
HRESULT _stdcall CWIADevice::drvGetWiaFormatInfo(
  BYTE            *pWiasContext,
  LONG            lFlags,
  LONG            *pcelt,
  WIA_FORMAT_INFO **ppwfi,
  LONG            *plDevErrVal)
{
    //
    // If the caller did not pass in the correct parameters,
    // then fail the call with E_INVALIDARG.
    //

    if ((!pWiasContext)||(!plDevErrVal)||(!pcelt)||(!ppwfi)) {
        return E_INVALIDARG;
    }

    //
    // check if WIA_FORMAT_INFO array has been initialized.
    //
    // NOTE: m_WIAFormatInfo is a member variable that has been
    //       defined as    WIA_FORMAT_INFO m_WIAFormatInfo[2];
    //
    //

    if (m_WIAFormatInfo[0].lTymed == TYMED_NULL) {

        //
        // add all supported formats and corresponding TYMED values
        // here
        //

        m_WIAFormatInfo[0].guidFormatID = WiaImgFmt_MEMORYBMP;
        m_WIAFormatInfo[0].lTymed       = TYMED_CALLBACK;

        m_WIAFormatInfo[1].guidFormatID = WiaImgFmt_BMP;
        m_WIAFormatInfo[1].lTymed       = TYMED_FILE;
    }

    *plDevErrVal = 0;
    *ppwfi = &m_WIAFormatInfo[0];
    *pcelt = 2; // number of formats in returned array

    return S_OK;
}
```

 

 




