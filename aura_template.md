# Aura Template
# 目次

#Lightning コンポーネント テンプレート
## Apexコントローラ

```
public with sharing class MyContactListController {
    @AuraEnabled
    public static List<Contact> getContacts(Id recordId) {
        return [
            SELECT
                Id,
                FirstName,
                LastName,
                Email,
                Phone
            FROM
                Contact
            WHERE
                AccountId = :recordId
        ];
    }
}
```

## コントローラ
- 

```
({
    myAction : function(component, event, helper) {
        // add code for the action
    },

    anotherAction : function(component, event, helper) {
        // more code
    },
})
```

### コーディング規約（案）
#### コントローラ.cls
- **[MUST]** 仮引数名はクライアント側でアクションを作成するときに使用するパラメータ名と一致させる。
- **[MUST]** コントローラ.jsのアクションハンドラの関数名と同じ名前のメソッドを使用しない。
#### コントローラ.js
- **[MUST]** アクションハンドラの仮引数は、component、event、helperをしようすること。
- **[MUST]** JSONオブジェクトの最後のアクションハンドラの後のカンマは省略しない。
- **[MUST]** コントローラ.clsのメソッド名と同じ名前のアクションハンドラの関数名を使用しない。
#### ヘルパー.js
- **[MUST]** 最初の引数はヘルパーを呼び出すコンポーネントへの参照であること。
- **[MUST]** JSONオブジェクトの最後のアクションハンドラの後のカンマは省略しない。