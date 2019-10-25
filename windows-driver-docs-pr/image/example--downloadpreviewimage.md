---
title: DownloadPreviewImage の例
description: DownloadPreviewImage の例
ms.assetid: 9b27492e-0725-4c8b-9101-3aaf5c9291d9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8664b629ab0925aa12bc612f423c077d9187b66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840840"
---
# <a name="example-downloadpreviewimage"></a>例: DownloadPreviewImage





**DownloadPreviewImage**関数は、プレビューコンポーネントの**Iwiapreview:: getnewpreview**メソッドを呼び出すことによって、スキャナーからイメージデータをダウンロードします。 次に、アプリケーションユーザーがセグメンテーションフィルターを呼び出す必要がある場合に、 **DetectSubregions**関数を呼び出します。これにより、検出された各リージョンの*pWiaItem2*に子項目が作成されます。 この例で使用されている**DetectSubregions**の詳細については、 [**IWiaSegmentationFilter::D etて region**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiasegmentationfilter-detectregions)メソッドを参照してください。

この例では、アプリケーションユーザーは、チェックボックスをオンにして、 *m\_bUseSegmentationFilter*パラメーターを設定します。 アプリケーションがこれをサポートしている場合は、まず、 **IWiaItem2:: CheckExtension**を呼び出して、ドライバーがセグメンテーションフィルターを持っていることを確認する必要があります。 この例で使用されている**CheckImgFilter**の詳細については、Microsoft Windows SDK ドキュメントの**Iwiapreview:: getnewpreview**メソッドを参照してください。

```cpp
HRESULT
DownloadPreviewImage(
  IN IWiaItem2 *pWiaFlatbedItem2)
{
  HRESULT              hr = S_OK;
  BOOL                 bHasImgFilter  = FALSE;
  IWiaTransferCallback *pAppWiaTransferCallback = NULL;

  hr = CheckImgFilter(pWiaFlatbedItem2, &bHasImgFilter)

  if (SUCCEEDED(hr))
  {
     if (bHasImgFilter)
     {
        IWiaPreview *pWiaPreview = NULL;

        // In this example, the AppWiaTransferCallback class 
        // implements the IWiaTransferCallback interface.
         // The constructor of AppWiaTransferCallback sets the 
         // reference count to 1.
         pAppWiaTransferCallback = new AppWiaTransferCallback();

         hr = pAppWiaTransferCallback ? S_OK : E_OUTOFMEMORY;

         if (SUCCEEDED(hr))
         {
            // Acquire image from scanner
            hr = m_pWiaPreview->GetNewPreview(pWiaFlatbedItem2,
                                              0,
                                              pAppWiaTransferCallback);    
         }

         // m_FlatbedPreviewStream is the stream that
         // AppWiaTransferCallback::GetNextStream returned for the
         // flatbed item.
         // This stream is where the image data is stored after
         // the successful return of GetNewPreview.
         // The stream is passed into the segmentation filter
         // for region detection.
         if (SUCCEEDED(hr) && m_bUseSegmentationFilter)
         {
            DetectSubregions(m_FlatbedPreviewStream, pWiaFlatbedItem2);
         }

         if (pAppWiaTransferCallback)
         {
            // If the call to GetNewPreview was successful, the
            // preview component calls AddRef on the callback so
            // this call doesn't delete the object.

            pAppWiaTransferCallback->Release();
         }

      }
      else
      {
         // Do not create an instance of preview component if the 
         // driver does not come with an image-processing filter.
         // You can use a segmentation filter, however, if the driver
         // comes with one (omitted here).
      }
   }

   return hr;
}
```

 

 




