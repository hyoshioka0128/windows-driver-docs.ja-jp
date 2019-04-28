---
title: データのメモリの割り当て
description: データのメモリの割り当て
ms.assetid: 15df5616-ddce-44ec-bd10-65cae0d95cf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5179716df822729294bf7c35291eb63b3bd89fcc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367078"
---
# <a name="allocating-memory-for-data"></a>データのメモリの割り当て





WIA サービスで提供される情報に依存、 [ **MINIDRV\_転送\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff545250)構造体を適切なデータ転送を実行します。 WIA ミニドライバーに関連するこの構造体のメンバーは次のとおりです。

**bClassDrvAllocBuf** − WIA サービス割り当てのブール値。

**pTransferBuffer**転送されたデータに割り当てられた − メモリへのポインター。

**lBufferSize** − メモリのサイズをによって示される、 **pTransferBuffer**メンバー。

場合、 **bClassDrvAllocBuf** 、MINIDRV のメンバー\_転送\_CONTEXT 構造体に設定されている**TRUE**、WIA サービスは、ミニドライバーのメモリを割り当てられています。 場合、 **bClassDrvAllocBuf**に設定されているメンバー **FALSE**、WIA サービス、ミニドライバーのメモリを割り当てられませんでした。

ミニドライバーは、使用してメモリを割り当てる必要があります、 **CoTaskMemAlloc**関数 (Microsoft Windows SDK のドキュメントで説明)。 ミニドライバーは内のメモリ位置へのポインターを格納する必要がありますし、 **pTransferBuffer**のメモリのサイズと**lBufferSize** (単位: バイト)。

**BClassDrvAllocBuff**に設定されているメンバー **FALSE**場合にのみ、 [ **WIA\_IPA\_TYMED** ](https://msdn.microsoft.com/library/windows/hardware/ff551656)プロパティは、TYMED に設定\_ファイルまたは TYMED\_マルチページ\_ファイル、および[ **WIA\_IPA\_項目\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551594)プロパティは、0 に設定されます。

ミニドライバーは overfill が指すバッファーにしないように注意する必要があります、 **pTransferBuffer**メンバー。 格納されている値未満の金額にデータを記述することでこれを回避する、 **lBufferSize**メンバー。

### <a name="enhancing-data-transfer-performance-by-using-minimum-buffer-size"></a>最小バッファー サイズを使用してデータ転送パフォーマンスの強化

WIA ミニドライバーは、設定によって、データ転送中に使用されるメモリの量を制御できます、 [ **WIA\_IPA\_項目\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551594)と[ **WIA\_IPA\_バッファー\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551527)プロパティ。

WIA アプリケーションを使用、WIA\_IPA\_バッファー\_サイズ プロパティをメモリ転送中に要求する最小の転送のバッファー サイズを確認します。 この値が大きいほど、要求されたバンドのサイズは大きくなります。 WIA アプリケーションを WIA の値より小さいサイズのバッファーを要求した場合\_IPA\_バッファー\_サイズ プロパティ、WIA サービスは、この要求のサイズを無視し、WIA ミニドライバーを求めるプロンプトのバッファーを WIA\_IPA\_バッファー\_サイズのバイト サイズ。 WIA サービスは常に、以上のバッファーを WIA ミニドライバーを要求 WIA\_IPA\_バッファー\_サイズのバイト サイズ。

**注**  値を WIA\_IPA\_バッファー\_サイズ プロパティが含まれていますが、最小限のデータの特定の時点でアプリケーションを要求できます。 バッファーのサイズは大きくなるほどの要求は、デバイスになります。 バッファー サイズが小さすぎるデータ転送のパフォーマンスが低下することができます。

 

WIA を設定することをお勧め\_IPA\_バッファー\_サイズ プロパティを効率的な速度でデータを転送するデバイスを許可する適切なサイズ。 これは、最適なパフォーマンスを確保するために分散要求 (バッファー サイズが小さすぎる) の数と時間のかかる要求 (バッファーは大きすぎます) デバイスの数。

設定する必要があります、 [ **WIA\_IPA\_項目\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551594) WIA ミニドライバーは、データを転送できる場合はゼロ プロパティ。 転送の種類が TYMED 場合\_ファイルまたは TYMED\_マルチページ\_ファイル、ミニドライバーの責任をファイルに書き込む WIA サービス関数に渡されるデータ バッファーのメモリを割り当てることができます。 これにより、一貫性の実装では、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)メソッド。

[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)メソッドは、デバイスからアプリケーションにデータを転送する予定の場合、WIA サービスによって呼び出されます。 WIA ドライバーは、アプリケーションが試みている (WIA サービス) 経由で転送の種類を参照して決定する必要があります、 **tymed**のメンバー、 [ **MINIDRV\_転送\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff545250):

**Tymed**アプリケーションで設定すると、メンバーには、次の 4 つの値のいずれかができます。

<a href="" id="tymed-file"></a>TYMED\_ファイル  
ファイルにデータを転送します。

<a href="" id="tymed-multipage-file"></a>TYMED\_マルチページ\_ファイル  
複数のファイル形式にデータを転送します。

<a href="" id="tymed-callback"></a>TYMED\_コールバック  
データをメモリに転送します。

<a href="" id="tymed-multipage-callback"></a>TYMED\_マルチページ\_コールバック  
複数のデータ ページをメモリに転送します。

さまざまなフラグ設定 XXX\_コールバックと XXX\_ファイルは、アプリケーションのコールバック インターフェイスを呼び出すことの使用法を変更します。

### <a href="" id="tymed-callback-and-tymed-multipage-callback"></a>TYMED\_コールバックと TYMED\_マルチページ\_コールバック

メモリの転送では、発行、 [ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff543946)コールバック。

(*pmdtc -&gt;pIWiaMiniDrvCallBack -&gt;MiniDrvCallback*で次のサンプル ソース コード)

次の値を使用してコールバックを行います。

<a href="" id="it-msg-data"></a>IT\_MSG\_データ  
ドライバーがデータを転送しています。

<a href="" id="it-status-transfer-to-client"></a>IT\_状態\_転送\_TO\_クライアント  
データは、メッセージを転送します。

<a href="" id="lpercentcomplete"></a>*lPercentComplete*  
完了している転送の割合。

<a href="" id="pmdtc--cboffset"></a>*pmdtc-&gt;cbOffset*  
アプリケーションが次のデータ チャンクを記述する場所の現在の場所には、これを更新します。

<a href="" id="lbytesreceived"></a>*lBytesReceived*  
アプリケーションに送信されるデータ チャンクのバイト数。

<a href="" id="pmdtc"></a>*pmdtc*  
ポインターを[ **MINIDRV\_転送\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff545250)データ転送の値を含む構造体。

### <a href="" id="tymed-file-and-tymed-multipage-file"></a>TYMED\_ファイルと TYMED\_マルチページ\_ファイル

ファイル転送では、発行、 [ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff543946)コールバック。

(*pmdtc -&gt;pIWiaMiniDrvCallBack -&gt;MiniDrvCallback*で次のサンプル ソース コード)

次の値を使用してコールバックを行います。

<a href="" id="it-msg-status"></a>IT\_MSG\_状態  
ドライバーは状態のみ (データなし) を送信しています。

<a href="" id="it-status-transfer-to-client"></a>IT\_状態\_転送\_TO\_クライアント  
データは、メッセージを転送します。

<a href="" id="lpercentcomplete"></a>*lPercentComplete*  
完了している転送の割合。

場合、 **ItemSize** 、MINIDRV のメンバー\_転送\_CONTEXT 構造体が 0 に設定されていることを WIA ドライバーは結果として得られるイメージのサイズがわからないし、その後割り当てます、独自アプリケーションを示しますデータ バッファー。 WIA ドライバーを読み込み、 [ **WIA\_IPA\_バッファー\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551527)プロパティ データの 1 つのバンドのメモリを割り当てるとします。 WIA ドライバーは、ここでは、必要なメモリの量を割り当てることができますが、割り当てが小規模で保持されることをお勧めします。

WIA サービスが、ドライバーのメモリを割り当てられたかどうかについては、確認、 *pmdtc -&gt;bClassDrvAllocBuf*フラグ。 設定されている場合**TRUE**、WIA サービスが、ドライバーのメモリを割り当て、します。 割り当てられたメモリの量を確認する、値をチェック*pmdtc -&gt;lBufferSize*します。

独自のメモリを割り当てるには、使用**CoTaskMemAlloc** (Microsoft Windows SDK のドキュメントで説明されている) にあるポインターを使用して、 *pmdtc -&gt;pTransferBuffer*します。 (ドライバーでは、ドライバーでは無料もする必要がありますので、このメモリが割り当てられていることに注意してください)。設定*pmdtc -&gt;lBufferSize*割り当てたサイズにします。 既に説明したとおり、この WIA サンプル ドライバーがバッファーのサイズ (バイト単位) に含まれている値と等しくを割り当てます[ **WIA\_IPA\_バッファー\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551527)します。 ドライバーは、そのメモリを使用します。

次の例の実装を示しています、 **IWiaMiniDrv::drvAcquireItemData**メソッド。 この例では、両方のメモリ割り当てのケースを処理できます。

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

 

 




