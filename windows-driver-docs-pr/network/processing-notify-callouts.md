---
title: 通知コールアウトの処理
description: 通知コールアウトの処理
ms.assetid: d686989e-97f0-4095-b172-1c2ccf7a26e6
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、コールアウトを通知します。
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームのコールアウトを通知します。
- notifyFn
- コールアウト WDK Windows フィルタ リング プラットフォームを通知します。
- Windows Filtering Platform コールアウト ドライバー WDK、フィルターの追加と削除
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームの追加と削除をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c8c1c6ef8155b032951d64458926aa991894737
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350361"
---
# <a name="processing-notify-callouts"></a>通知コールアウトの処理


フィルター エンジン呼び出し吹き出しの[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)コールアウト関数引き出し線に関連付けられているイベントに関するコールアウト ドライバーに通知します。

### <a href="" id="filter-addition"></a> フィルターの追加

呼び出すときに、フィルターのアクションが、フィルター エンジンに追加された場合、引き出し線を指定するフィルター、フィルター エンジン吹き出しの[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)コールアウト関数を FWPS\_コールアウト\_通知\_追加\_でフィルター処理、 *notifyType*パラメーター。

コールアウト ドライバーは、フィルターのアクションの引き出し線を指定するフィルターをフィルター エンジンに既に追加した後、フィルター エンジンを吹き出しを登録できます。 このような状況で、フィルター エンジンは呼び出しません吹き出しの[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)コールアウト関数について、既存のフィルターのいずれかの吹き出しに通知します。

フィルター エンジンは吹き出しののみを呼び出して*notifyFn*コールアウト関数に、フィルターのアクションの引き出し線を指定する新しいフィルターがフィルター エンジンに追加されたときに、引き出し線を通知します。 このような状況で、吹き出しの*notifyFn*フィルターのアクションの引き出し線を指定するフィルター エンジンですべてのフィルターのコールアウト関数を呼び出さない可能性があります。

コールアウト ドライバーは、フィルター エンジンが起動し、引き出し線は、フィルターのアクションの引き出し線を指定するフィルター エンジンですべてのフィルターに関する情報を受け取る必要があります。、吹き出しを登録、コールアウト ドライバーは適切な管理を呼び出す必要があります。フィルター エンジンのすべてのフィルターを列挙する機能です。 コールアウト ドライバーは、これらのフィルターのアクションの引き出し線を指定するフィルターを検索するすべてのフィルターの結果の一覧を並べ替える必要があります。 参照してください[その他の Windows フィルタ リング プラットフォーム関数の呼び出し](calling-other-windows-filtering-platform-functions.md)詳細については、これらの関数を呼び出すことです。

### <a href="" id="filter-deletion"></a> フィルターの削除

呼び出すときに、フィルターのアクションは、フィルター エンジンから削除された吹き出しを指定するフィルター、フィルター エンジン吹き出しの[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)コールアウト関数を渡します FWPS\_吹き出し\_通知\_削除\_でフィルター処理、 *notifyType*パラメーターと**NULL**で、 *filterKey*パラメーター。 フィルター エンジンの呼び出しのコールアウトの*notifyFn*フィルターのアクションの引き出し線を指定するフィルター エンジンですべて削除されたフィルターの吹き出し関数。 これには、コールアウト ドライバーは、フィルター エンジンの引き出し線を登録する前に、フィルター エンジンに追加されたすべてのフィルターが含まれます。 そのため、コールアウトは、通知を追加するフィルターのフィルターの受け取らなかったために、フィルター削除通知を受け取る可能性があります。

場合吹き出しの[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)コールアウト関数に渡される通知の種類を認識しません、 *notifyType*パラメーターを無視すること、通知と状態の戻り値\_成功します。

コールアウト ドライバーでは、フィルター エンジンに追加されると、フィルター、フィルターに関連するコンテキストを指定できます。 このようなコンテキストでは、フィルター エンジンに対して非透過的です。 吹き出しの[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)コールアウト関数は、このコンテキストを使用して、フィルター エンジンによって呼び出されたときに [次へ] に状態情報を保存します。 フィルター エンジンからフィルターを削除すると、コールアウト ドライバーは、コンテキストのために必要なクリーンアップを実行します。

例:

```C++
// Context structure to be associated with the filters
typedef struct FILTER_CONTEXT_ {
  .
  .  // Driver-specific content
  .
} FILTER_CONTEXT, *PFILTER_CONTEXT;

// Memory pool tag for filter context structures
#define FILTER_CONTEXT_POOL_TAG 'fcpt'

// notifyFn callout function
NTSTATUS NTAPI
 NotifyFn(
    IN FWPS_CALLOUT_NOTIFY_TYPE  notifyType,
    IN const GUID  *filterKey,
    IN const FWPS_FILTER0  *filter
    )
{
  PFILTER_CONTEXT context;

 ASSERT(filter != NULL);

  // Switch on the type of notification
 switch(notifyType) {

    // A filter is being added to the filter engine
 case FWPS_CALLOUT_NOTIFY_ADD_FILTER:

      // Allocate the filter context structure
 context =
        (PFILTER_CONTEXT)ExAllocatePoolWithTag(
 NonPagedPool,
 sizeof(FILTER_CONTEXT),
          FILTER_CONTEXT_POOL_TAG
          );

      // Check the result of the memory allocation
 if (context == NULL) {

        // Return error
 return STATUS_INSUFFICIENT_RESOURCES;
      }

      // Initialize the filter context structure
      ...

      // Associate the filter context structure with the filter
 filter->context = (UINT64)context;

 break;

    // A filter is being removed from the filter engine
 case FWPS_CALLOUT_NOTIFY_DELETE_FILTER:

      // Get the filter context structure from the filter
 context = (PFILTER_CONTEXT)filter->context;

 // Check whether the filter has a context
 if (context) {

        // Cleanup the filter context structure
        ...

        // Free the memory for the filter context structure
 ExFreePoolWithTag(
 context,
          FILTER_CONTEXT_POOL_TAG
          );

      }
 break;

    // Unknown notification
 default:

      // Do nothing
 break;
  }

 return STATUS_SUCCESS;
}
```

 

 





