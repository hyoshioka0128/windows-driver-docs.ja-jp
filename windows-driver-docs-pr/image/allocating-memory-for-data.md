---
title: データのメモリの割り当て
description: データのメモリの割り当て
ms.assetid: 15df5616-ddce-44ec-bd10-65cae0d95cf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c85eeb041a5f53b999f86ffd7ed66dbcecfca3f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840901"
---
# <a name="allocating-memory-for-data"></a>データのメモリの割り当て





WIA サービスは、 [**MINIDRV\_TRANSFER\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)構造に指定された情報に依存して、適切なデータ転送を実行します。 この構造体のうち、WIA ミニドライバーに関連するメンバーは次のとおりです。

**Bclassdrvallocbuf** − WIA サービスの割り当てのブール値。

**Ptransferbuffer** : 転送されたデータに割り当てられたメモリへのポインター。

**Lbuffersize** − **ptransferbuffer**メンバーが指すメモリのサイズ。

MINIDRV\_TRANSFER\_CONTEXT 構造体の**Bclassdrvallocbuf**メンバーが**TRUE**に設定されている場合、WIA サービスはミニドライバーに割り当てられたメモリを使用します。 **Bclassdrvallocbuf**メンバーが**FALSE**に設定されている場合、WIA サービスはミニドライバーにメモリを割り当てませんでした。

ミニドライバーは、 **CoTaskMemAlloc**関数 (Microsoft Windows SDK のドキュメントで説明) を使用してメモリを割り当てる必要があります。 ミニドライバーは、 **Ptransferbuffer**内のメモリ位置へのポインターと、 **lbuffersize** (バイト単位) のメモリのサイズを格納する必要があります。

**Bclassdrvallocbuff**メンバーが**FALSE**に設定されるのは、 [**wia\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)プロパティが tymed\_file または tymed\_MULTIPAGE\_file、および[**wia\_IPA\_ITEM に設定されている場合のみ\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)プロパティが0に設定されています。

ミニドライバーは、 **Ptransferbuffer**メンバーが指すバッファーをオーバーフィルしないように注意する必要があります。 これを回避するには、 **Lbuffersize**メンバーに格納されている値以下の量のデータを書き込みます。

### <a name="enhancing-data-transfer-performance-by-using-minimum-buffer-size"></a>最小バッファーサイズを使用してデータ転送パフォーマンスを向上させる

Wia ミニドライバーは、データ転送中に使用されるメモリの量を制御できます。これを行うには、 [**wia\_IPA\_ITEM\_size**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)および[**wia\_IPA\_BUFFER\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)プロパティを設定します。

WIA アプリケーションでは、WIA\_IPA\_BUFFER\_SIZE プロパティを使用して、メモリ転送中に要求する転送バッファーの最小サイズを決定します。 この値が大きいほど、要求された帯域幅が大きくなります。 Wia アプリケーションが、WIA\_IPA\_BUFFER\_SIZE プロパティの値よりも小さいサイズのバッファーを要求した場合、WIA サービスはこの要求されたサイズを無視し、wia ミニドライバーに対して wia\_IPA のバッファーを要求し\_バッファー\_サイズのバイト数。 Wia サービスは、wia ミニドライバーに対して、少なくとも WIA\_IPA\_バッファー\_サイズバイト単位のバッファーを要求します。

**   "** WIA\_IPA\_BUFFER\_SIZE" プロパティに含まれる値は、アプリケーションが任意の時点で要求できるデータの最小量です。 バッファーサイズが大きいほど、デバイスに対する要求が大きくなります。 バッファーサイズが小さすぎると、データ転送のパフォーマンスが低下する可能性があります。

 

デバイスが効率的な速度でデータを転送できるようにするには、WIA\_IPA\_BUFFER\_SIZE プロパティを妥当なサイズに設定することをお勧めします。 これを行うには、最適なパフォーマンスを得るために、要求の数 (バッファーサイズが小さすぎません) と、デバイスの時間がかかる要求 (バッファーが大きすぎます) の数を分散します。

WIA ミニドライバーでデータを転送できる場合は、 [**wia\_IPA\_ITEM\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-size)プロパティを0に設定する必要があります。 転送の種類が\_FILE または TYMED\_マルチページ\_ファイルの場合、ファイルに書き込む WIA サービス関数に渡されるデータバッファーにメモリを割り当てることはミニドライバーの責任です。 これにより、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドの実装に一貫性が確保されます。

[**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドは、デバイスからアプリケーションにデータを転送する予定の場合に、WIA サービスによって呼び出されます。 WIA ドライバーでは、アプリケーションが実行しようとしている転送の種類を特定する必要があります。そのためには、 [**MINIDRV\_transfer\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)の**tymed**メンバーを読み取ります。

アプリケーションによって設定される**tymed**メンバーは、次の4つの値のいずれかを持つことができます。

<a href="" id="tymed-file"></a>TYMED\_ファイル  
データをファイルに転送します。

<a href="" id="tymed-multipage-file"></a>TYMED\_マルチページ\_ファイル  
データを複数ページのファイル形式に転送します。

<a href="" id="tymed-callback"></a>TYMED\_コールバック  
メモリにデータを転送します。

<a href="" id="tymed-multipage-callback"></a>TYMED\_マルチページ\_コールバック  
複数のページのデータをメモリに転送します。

異なる TYMED 設定 XXX\_CALLBACK と XXX\_ファイルは、アプリケーションのコールバックインターフェイスの呼び出しの使用方法を変更します。

### <a href="" id="tymed-callback-and-tymed-multipage-callback"></a>TYMED\_コールバックと TYMED\_マルチページ\_コールバック

メモリ転送の場合は、 [**IWiaMiniDrvCallBack:: MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)コールバックを発行します。

(次のサンプルソースコードの*pmdtc-&gt;pIWiaMiniDrvCallBack-&gt;MiniDrvCallback* )

次の値を使用してコールバックを作成します。

<a href="" id="it-msg-data"></a>\_MSG\_データ  
ドライバーがデータを転送しています。

<a href="" id="it-status-transfer-to-client"></a>\_を\_クライアントに転送\_状態を\_します。  
データ転送メッセージ。

<a href="" id="lpercentcomplete"></a>*lPercentComplete 率*  
転送が完了した割合。

<a href="" id="pmdtc--cboffset"></a>*pmdtc-&gt;cbOffset*  
アプリケーションが次のデータチャンクを書き込む必要がある現在の場所にこれを更新します。

<a href="" id="lbytesreceived"></a>*受信した lbytes*  
アプリケーションに送信されるデータチャンク内のバイト数。

<a href="" id="pmdtc"></a>*pmdtc*  
データ転送値を格納する[**コンテキスト構造\_MINIDRV\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)へのポインター。

### <a href="" id="tymed-file-and-tymed-multipage-file"></a>\_ファイルと TYMED\_マルチページ\_ファイル

ファイル転送の場合は、 [**IWiaMiniDrvCallBack:: MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback) callback:: を発行します。

(次のサンプルソースコードの*pmdtc-&gt;pIWiaMiniDrvCallBack-&gt;MiniDrvCallback* )

次の値を使用してコールバックを作成します。

<a href="" id="it-msg-status"></a>\_MSG\_STATUS  
ドライバーは状態のみを送信しています (データなし)。

<a href="" id="it-status-transfer-to-client"></a>\_を\_クライアントに転送\_状態を\_します。  
データ転送メッセージ。

<a href="" id="lpercentcomplete"></a>*lPercentComplete 率*  
転送が完了した割合。

MINIDRV\_TRANSFER\_CONTEXT 構造体の**Itemsize**メンバーが0に設定されている場合、これは、WIA ドライバーが結果のイメージサイズを認識せず、独自のデータバッファーを割り当てることをアプリケーションに示します。 WIA ドライバーは、 [**wia\_IPA\_BUFFER\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)プロパティを読み取り、1つのデータバンドにメモリを割り当てます。 WIA ドライバーは、ここで必要な量のメモリを割り当てることができますが、割り当てを小さくすることをお勧めします。

WIA サービスにドライバーのメモリが割り当てられているかどうかを確認するには、 *pmdtc-&gt;bClassDrvAllocBuf*フラグをチェックします。 **TRUE**に設定されている場合、WIA サービスはドライバー用にメモリを割り当てました。 割り当てられたメモリの量を確認するには、 *pmdtc-&gt;lBufferSize*の値を確認します。

独自のメモリを割り当てるには、(Microsoft Windows SDK のドキュメントで説明されている) **CoTaskMemAlloc**を使用して、 *pmdtc-&gt;pmdtc*にあるポインターを使用します。 (ドライバーによってこのメモリが割り当てられていることに注意してください。そのため、ドライバーも解放する必要があります)。*Pmdtc-&gt;lBufferSize*を、割り当てたサイズに設定します。 既に説明したように、この WIA サンプルドライバーは、サイズをバイト単位で格納するバッファーを、 [**wia\_IPA\_buffer\_size**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)に格納されている値と同一に割り当てます。 その後、ドライバーはそのメモリを使用します。

**IWiaMiniDrv::D rvacquireitemdata**メソッドの実装例を次に示します。 この例では、両方のメモリ割り当てケースを処理できます。

```cpp
HRESULT _stdcall CWIADevice::drvAcquireItemData(
  BYTE                      *pWiasContext,
  LONG                      lFlags,
  PMINIDRV_TRANSFER_CONTEXT pmdtc,
  LONG                      *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if (!pWiasContext) {
    return E_INVALIDARG;
  }

  if (!pmdtc) {
    return E_INVALIDARG;
  }

  if (!plDevErrVal) {
    return E_INVALIDARG;
  }

  *plDevErrVal = 0;

  HRESULT hr = E_FAIL;
  LONG lBytesTransferredToApplication = 0;
  LONG lClassDrvAllocSize = 0;
  //
  // (1) Memory allocation
  //

  if (pmdtc->bClassDrvAllocBuf) {

    //
    // WIA allocated the buffer for data transfers
    //

    lClassDrvAllocSize = pmdtc->lBufferSize;
    hr = S_OK;
  } else {

    //
    // Driver allocated the buffer for data transfers
    //

    hr = wiasReadPropLong(pWiasContext, WIA_IPA_BUFFER_SIZE, &lClassDrvAllocSize,NULL,TRUE);
    if (FAILED(hr)) {

      //
      // no memory was allocated, here so we can return early
      //

      return hr;
    }

    //
    // allocate memory of WIA_IPA_BUFFER_SIZE (own min buffer size)
    //

    pmdtc->pTransferBuffer = (PBYTE) CoTaskMemAlloc(lClassDrvAllocSize);
    if (!pmdtc->pTransferBuffer) {

      //
      // no memory was allocated, here so we can return early
      //

      return E_OUTOFMEMORY;
    }

    //
    // set the lBufferSize member
    //

    pmdtc->lBufferSize = lClassDrvAllocSize;
  }

  //
  // (2) Gather all information about data transfer settings and
  //     calculate the total data amount to transfer
  //

  if (hr == S_OK) {
    //
    // WIA service will populate the MINIDRV_TRANSFER_CONTEXT by reading the WIA properties.
    //
    // The following values will be written as a result of the 
    // wiasGetImageInformation() call
    //
    // pmdtc->lWidthInPixels
    // pmdtc->lLines
    // pmdtc->lDepth
    // pmdtc->lXRes
    // pmdtc->lYRes
    // pmdtc->lCompression
    // pmdtc->lItemSize
    // pmdtc->guidFormatID
    // pmdtc->tymed
    //
    // if the FORMAT is set to BMP or MEMORYBMP, the
    // following values will also be set automatically
    //
    // pmdtc->cbWidthInBytes
    // pmdtc->lImageSize
    // pmdtc->lHeaderSize
    // pmdtc->lItemSize (will be updated using the known image format information)
    //

    hr = wiasGetImageInformation(pWiasContext,0,pmdtc);
    if (hr == S_OK) {

      //
      // (3) Send the image data to the application
      //

      LONG lDepth = 0;
      hr = wiasReadPropLong(pWiasContext, WIA_IPA_DEPTH, &lDepth,NULL,TRUE);
      if (hr == S_OK) {

        LONG lPixelsPerLine = 0;
        hr = wiasReadPropLong(pWiasContext, WIA_IPA_PIXELS_PER_LINE, &lPixelsPerLine,NULL,TRUE);
        if (hr == S_OK) {

            LONG lBytesPerLineRaw     = ((lPixelsPerLine * lDepth) + 7) / 8;
            LONG lBytesPerLineAligned = (lPixelsPerLine * lDepth) + 31;
            lBytesPerLineAligned      = (lBytesPerLineAligned / 8) & 0xfffffffc;
            LONG lTotalImageBytes     = pmdtc->lImageSize + pmdtc->lHeaderSize;
            LONG lBytesReceived       = pmdtc->lHeaderSize;
            lBytesTransferredToApplication = 0;
            pmdtc->cbOffset = 0;

            while ((lBytesReceived)) {

              LONG lPercentComplete = (LONG)(((float)lBytesTransferredToApplication/(float)lTotalImageBytes) * 100.0f);
              switch (pmdtc->tymed) {
              case TYMED_MULTIPAGE_CALLBACK:
              case TYMED_CALLBACK:
                {
                  hr = pmdtc->pIWiaMiniDrvCallBack->MiniDrvCallback(IT_MSG_DATA,IT_STATUS_TRANSFER_TO_CLIENT,
                                                                  lPercentComplete,pmdtc->cbOffset,lBytesReceived,pmdtc,0);
                pmdtc->cbOffset += lBytesReceived;
                lBytesTransferredToApplication += lBytesReceived;
           }
            break;
          case TYMED_MULTIPAGE_FILE:
          case TYMED_FILE:
            {
                //
                // lItemSize is the amount that wiasWriteBufToFile will write to FILE
                //

                pmdtc->lItemSize = lBytesReceived;
                hr = wiasWriteBufToFile(0,pmdtc);
                if (FAILED(hr)) {
                    break;
                }

                hr = pmdtc->pIWiaMiniDrvCallBack->MiniDrvCallback(IT_MSG_STATUS,IT_STATUS_TRANSFER_TO_CLIENT,
                                                                  lPercentComplete,0,0,NULL,0);
                lBytesTransferredToApplication += lBytesReceived;
              }
              break;
          default:
              {
          hr = E_FAIL;
              }
              break;
          }

          //
          // scan from device, requesting ytesToReadFromDevice
          //

          LONG lBytesRemainingToTransfer = (lTotalImageBytes - lBytesTransferredToApplication);
          if (lBytesRemainingToTransfer <= 0) {
              break;
            }

            //
            // calculate number of bytes to request from device
            //

            LONG lBytesToReadFromDevice = (lBytesRemainingToTransfer > pmdtc->lBufferSize) ? pmdtc->lBufferSize : lBytesRemainingToTransfer;

            // RAW data request
            lBytesToReadFromDevice = (lBytesToReadFromDevice / lBytesPerLineAligned) * lBytesPerLineRaw;

            // Aligned data request
            // lBytesToReadFromDevice = (lBytesToReadFromDevice / lBytesPerLineAligned) * lBytesPerLineAligned;

            if ((hr == S_FALSE)||FAILED(hr)) {

              //
              // user canceled or the callback failed for some reason
              //

              break;
            }

            //
            // request byte amount from device
            //

            hr = GetDataFromMyDevice(pmdtc->pTransferBuffer, lBytesToReadFromDevice, (DWORD*)&lBytesReceived);
            if (FAILED(hr)) {
                break;
            }

            //
            // this device returns raw data.  If your device does this too, then you should call the AlignInPlace
            // helper function to align the data.
            //

            lBytesReceived = AlignMyRawData(pmdtc->pTransferBuffer,lBytesReceived,lBytesPerLineAligned,lBytesPerLineRaw);

          } // while ((lBytesReceived))
        }
      }
    }
  }

  //
  // free any allocated memory for buffers
  //

  if (!pmdtc->bClassDrvAllocBuf) {
    CoTaskMemFree(pmdtc->pTransferBuffer);
    pmdtc->pTransferBuffer = NULL;
    pmdtc->lBufferSize = 0;
  }

  return hr;
}
```

 

 




