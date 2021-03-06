---
title: イメージ形式のサポートの追加
description: イメージ形式のサポートの追加
ms.assetid: 1ffa7c0d-23ec-402a-a0b5-fb5596a851bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4cb2a158955cf46959f3efbfb81694938309c41
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375937"
---
# <a name="adding-image-format-support"></a>イメージ形式のサポートの追加





WIA ミニドライバー WIA サービスへのイメージ形式のレポート、 [ **IWiaMiniDrv::drvGetWiaFormatInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)メソッド。

### <a href="" id="implementing-iwiaminidrv-drvgetwiaformatinfo"></a>Implementing IWiaMiniDrv::drvGetWiaFormatInfo

WIA サービスの呼び出し、 **IWiaMiniDrv::drvGetWiaFormatInfo** WIA デバイスでサポートされているフラグと形式のペアを取得します。

(この WIA ドライバーに格納され、この WIA ドライバーによって解放される) にメモリを割り当てる必要があります、WIA ドライバー WIA の配列を含める\_形式\_情報の構造 (Microsoft Windows SDK のドキュメントで説明)。 WIA ドライバーに割り当てられたメモリへのポインターを渡す必要があります*ppwfi*します。 直接的にではがポインターにポインターを使用して、この操作は行われません。 次の例では、 *ppwfi* m のアドレスが設定されている\_WIAFormatInfo\[0\]、さらに、構造体の最初のメンバーのアドレスに評価されます。

WIA サービスはこのメモリを解放していないことに注意してください。 重要です。 この割り当てられたメモリを管理する WIA ドライバーの役目です。

WIA ドライバーは、メモリ位置に割り当てられている構造体の数を書き込む必要があります、 *pcelt*パラメーター ポイント。

WIA デバイスを設定する必要があります、 **guidFormatID** 、WIA のメンバー\_形式\_イメージ形式の GUID に情報の構造体。 デバイスを設定する必要があります、 **lTymed** TYMED 値にこの構造体のメンバーは、イメージ形式の GUID に関連付けられています。

有効なフラグ値 ("Media Type"とも呼ばれます) は次のとおりです。

TYMED\_ファイル

TYMED\_マルチページ\_ファイル

TYMED\_コールバック

TYMED\_マルチページ\_コールバック

次の例の実装を示しています[ **IWiaMiniDrv::drvGetWiaFormatInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo):。

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

 

 




