---
title: 通知コールアウトの処理
description: 通知コールアウトの処理
ms.assetid: d686989e-97f0-4095-b172-1c2ccf7a26e6
keywords:
- Windows フィルタリングプラットフォームコールアウトドライバー WDK、通知吹き出し
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、コールアウト通知
- notifyFn
- 吹き出しを通知する WDK Windows フィルタリングプラットフォーム
- Windows フィルタリングプラットフォームのコールアウトドライバーの WDK、フィルターの追加と削除
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、フィルターの追加と削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47dc589056f07b755dd456c25560799919786aab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843485"
---
# <a name="processing-notify-callouts"></a>通知コールアウトの処理


フィルターエンジンは、コールアウトの[*Notifyfn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)コールアウト関数を呼び出して、コールアウトに関連付けられているイベントについてコールアウトドライバーに通知します。

### <a href="" id="filter-addition"></a>フィルターの追加

フィルターのアクションのコールアウトを指定するフィルターがフィルターエンジンに追加されると、フィルターエンジンはコールアウトの[*Notifyfn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)コールアウト関数を呼び出し、fwps\_コールアウト\_通知し、\_\_フィルターを追加します *。notifyType*パラメーター。

フィルターのアクションのコールアウトを指定するフィルターが既にフィルターエンジンに追加されている場合、コールアウトドライバーはフィルターエンジンにコールアウトを登録できます。 このような状況では、フィルターエンジンは、既存のフィルターについてコールアウトに通知するために、コールアウトの[*Notifyfn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)コールアウト関数を呼び出しません。

フィルターエンジンは、コールアウトの*Notifyfn*コールアウト関数だけを呼び出して、フィルターのアクションのコールアウトを指定する新しいフィルターがフィルターエンジンに追加されたときに、コールアウトを通知します。 このような状況では、フィルターのアクションのコールアウトを指定するフィルターエンジン内のすべてのフィルターに対して、コールアウトの*Notifyfn*コールアウト関数が呼び出されないことがあります。

フィルターエンジンの起動後にコールアウトドライバーがコールアウトを登録し、フィルターのアクションのコールアウトを指定するフィルターエンジンのすべてのフィルターに関する情報をコールアウトが受信する必要がある場合は、コールアウトドライバーが適切な管理を呼び出す必要があります。フィルターエンジン内のすべてのフィルターを列挙する関数。 コールアウトドライバーは、フィルターのアクションのコールアウトを指定するフィルターを見つけるために、結果として得られるすべてのフィルターの一覧を並べ替える必要があります。 これらの関数の呼び出しの詳細については、「[その他の Windows フィルタリングプラットフォーム関数の呼び出し](calling-other-windows-filtering-platform-functions.md)」を参照してください。

### <a href="" id="filter-deletion"></a>フィルターの削除

フィルターのアクションのコールアウトを指定するフィルターがフィルターエンジンから削除されると、フィルターエンジンは、コールアウトの[*Notifyfn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)コールアウト関数を呼び出して、fwps\_コールアウト\_通知\_削除\_フィルターを*filterKey*パラメーターで*notifytype*パラメーターと**NULL**を指定します。 フィルターエンジンは、フィルターエンジン内の削除されたすべてのフィルターに対して*コールアウト関数*を呼び出し、フィルターのアクションのコールアウトを指定します。 これには、コールアウトドライバーがコールアウトをフィルターエンジンに登録する前にフィルターエンジンに追加されたフィルターが含まれます。 そのため、コールアウトはフィルターの削除通知を受け取ることがあります。フィルターは、フィルターの追加通知を受信しませんでした。

*Notifyfn*パラメーターで渡される通知の種類がコールアウトの[*notifyfn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)コールアウト関数によって認識されない場合は、通知を無視し、状態\_SUCCESS に戻す必要があります。

フィルターがフィルターエンジンに追加されると、コールアウトドライバーはフィルターに関連付けられるコンテキストを指定できます。 このようなコンテキストは、フィルターエンジンに対して非透過的です。 コールアウトの[*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)関数は、このコンテキストを使用して、フィルターエンジンによって次回呼び出されたときの状態情報を保存できます。 フィルターがフィルターエンジンから削除されると、コールアウトドライバーはコンテキストの必要なクリーンアップを実行します。

次に、例を示します。

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

 

 





