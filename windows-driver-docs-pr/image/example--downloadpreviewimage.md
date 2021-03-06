---
title: 例 DownloadPreviewImage
description: 例 DownloadPreviewImage
ms.assetid: 9b27492e-0725-4c8b-9101-3aaf5c9291d9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84238d4f1e3f5527f9fb9d45ab4ed18b7a7d3794
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372590"
---
# <a name="example-downloadpreviewimage"></a>以下に例を示します。DownloadPreviewImage





**DownloadPreviewImage**関数は、プレビューのコンポーネントを呼び出すことによって、スキャナーからイメージ データをダウンロード**IWiaPreview::GetNewPreview**メソッド。 呼び出して、 **DetectSubregions**アプリケーションのユーザーは、下の子項目を作成する、セグメント化フィルターを呼び出す必要がある場合に機能*pWiaItem2*が検出した地域ごとにします。 について**DetectSubregions**、この例で使用されるを参照してください、 [ **IWiaSegmentationFilter::DetectRegions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwiasegmentationfilter-detectregions)メソッド。

この例では、アプリケーションのユーザーの設定、 *m\_bUseSegmentationFilter*パラメーター チェック ボックスをオンします。 ドライバーが呼び出すことによってセグメント化フィルターを持っていることを確認、アプリケーションでは、これをサポートする場合最初必要があります**IWiaItem2::CheckExtension**します。 について**CheckImgFilter**、この例で使用されるを参照してください、 **IWiaPreview::GetNewPreview** Microsoft Windows SDK のドキュメント内のメソッド。

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

 

 




