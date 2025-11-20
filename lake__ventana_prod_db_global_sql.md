```mermaid
erDiagram
    %% =======================================================
    %% Global Configuration & Masters (prod_db_global_sql_)
    %% =======================================================

    prod_db_global_sql_bo_account_master {
        INTEGER id PK "BOアカウントマスターID"
        STRING auth_name "権限名"
    }
    prod_db_global_sql_bo_language_master {
        INTEGER id PK "BO言語マスターID"
        STRING locale "ロケール"
    }
    prod_db_global_sql_bo_account_info_status {
        INTEGER id PK "BOアカウント情報ステータスID"
        STRING status_code "ステータスコード"
    }
    prod_db_global_sql_bo_color_master {
        INTEGER id PK "BO色マスターID"
        STRING color_code_name "カラーコード名"
    }
    prod_db_global_sql_bo_account_info {
        INTEGER id PK "ID"
        INTEGER FK_bo_account_info_status_id FK "BOアカウント情報ステータスID"
        INTEGER FK_bo_account_master_id FK "BOアカウントマスターID"
        INTEGER FK_bo_language_master_id FK "BO言語マスターID"
        STRING mail_address "メールアドレス"
    }
    prod_db_global_sql_bo_access_key_info {
        INTEGER id PK "ID"
        INTEGER FK_bo_account_info_id FK "BOアカウント情報ID"
        STRING access_key "アクセスキー"
    }
    prod_db_global_sql_bo_account_info_status_color_mapping {
        INTEGER FK_bo_account_info_status_id PK "BOアカウント情報ステータスID"
        INTEGER FK_bo_color_master_id PK "BO色マスターID"
    }

    prod_db_global_sql_bo_corporation_info_status {
        INTEGER id PK "BO法人情報ステータスID"
        STRING status_code "ステータスコード"
    }
    prod_db_global_sql_bo_corporation_info_status_color_mapping {
        INTEGER FK_bo_corporation_info_status_id PK "BO法人情報ステータスID"
        INTEGER FK_bo_color_master_id PK "BO色マスターID"
    }
    
    prod_db_global_sql_engine_server_info {
        INTEGER id PK "ID"
        STRING authentication "認証エンドポイント"
    }
    prod_db_global_sql_server_region_info {
        INTEGER id PK "ID"
        INTEGER FK_engine_server_info_id FK "エンジンサーバー情報ID"
        STRING server_region_name "サーバーリージョン名"
    }
    prod_db_global_sql_master_corporation_info {
        INTEGER id PK "ID"
        INTEGER FK_bo_corporation_info_status_id FK "BO法人情報ステータスID"
        INTEGER FK_server_region_info_id FK "サーバーリージョン情報ID"
        STRING corp_id "法人ID"
    }
    
    prod_db_global_sql_sales_region_info {
        INTEGER id PK "ID"
        STRING sales_region_name "販売リージョン名"
    }
    prod_db_global_sql_region_mapping_info {
        INTEGER FK_server_region_info_id PK "サーバーリージョン情報ID"
        INTEGER FK_sales_region_info_id PK "販売リージョン情報ID"
    }
    
    prod_db_global_sql_url_type {
        INTEGER id PK "ID"
        STRING name "URLタイプ名"
    }
    prod_db_global_sql_url_info {
        INTEGER FK_server_region_info_id PK "サーバーリージョン情報ID"
        INTEGER FK_url_type_id PK "URLタイプID"
        STRING url "URL"
    }
    
    prod_db_global_sql_master_device_mode {
        INTEGER id PK "ID"
        INTEGER mode_id "モードID"
    }
    prod_db_global_sql_serial_info_master {
        INTEGER id PK "ID"
        INTEGER FK_corp_id FK "法人ID"
        INTEGER FK_sales_region_id FK "販売リージョンID"
        INTEGER FK_server_region_id FK "サーバーリージョンID"
        INTEGER FK_master_device_mode_id FK "デバイスモードマスターID"
        STRING imei1 "IMEI1"
    }

    prod_db_global_sql_device_public_secret_key_info {
        INTEGER id PK "ID"
        INTEGER FK_serial_info_master_id FK "シリアル情報マスターID"
        STRING public_key "公開鍵"
    }
    prod_db_global_sql_device_url_control_info {
        INTEGER id PK "ID"
        INTEGER FK_master_serial_info_id FK "シリアル情報マスターID"
    }
    prod_db_global_sql_device_authentication_key {
        INTEGER id PK "ID"
        STRING public_key "公開鍵"
    }
    
    prod_db_global_sql_bo_serial_import_history_info_status {
        INTEGER id PK "ID"
        STRING status_code "ステータスコード"
    }
    prod_db_global_sql_bo_serial_import_history_info {
        INTEGER id PK "ID"
        INTEGER FK_master_corporation_info_id FK "法人情報マスターID"
        INTEGER FK_bo_serial_import_history_info_status_id FK "ステータスID"
        STRING order_id "注文ID"
    }
    prod_db_global_sql_bo_serial_import_history_info_status_color_mapping {
        INTEGER id PK "ID"
    }
    prod_db_global_sql_bo_shipping_file_detail {
        INTEGER id PK "ID"
    }
    prod_db_global_sql_bo_tmp_serial_info_detail {
        INTEGER id PK "ID"
    }
    prod_db_global_sql_sfdc_export_csv_info {
        INTEGER id PK "ID"
    }

    %% =======================================================
    %% Temporary/Operational Tables (temp_prod_db_)
    %% =======================================================

    temp_prod_db_language_master {
        INTEGER id PK "言語マスターID"
        STRING locale "ロケール"
    }
    temp_prod_db_language_code_master {
        INTEGER id PK "ID"
        INTEGER FK_language_master_id FK "言語マスターID"
    }
    temp_prod_db_role_info {
        INTEGER id PK "ロール情報ID"
        STRING role_name "ロール名"
    }
    temp_prod_db_account_info_status {
        INTEGER id PK "アカウントステータスID"
        STRING status_code "ステータスコード"
    }
    temp_prod_db_color_master {
        INTEGER id PK "色マスターID"
    }
    temp_prod_db_corporation_info_status {
        INTEGER id PK "法人ステータスID"
        STRING status_code "ステータスコード"
    }
    temp_prod_db_corporation_info {
        INTEGER id PK "ID"
        INTEGER Fk_corporation_info_status_id FK "法人情報ステータスID"
        STRING corp_id "法人ID"
    }
    temp_prod_db_account_info {
        INTEGER id PK "ID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
        INTEGER FK_role_info_id FK "ロール情報ID"
        INTEGER FK_language_master_id FK "言語マスターID"
        INTEGER FK_account_info_status_id FK "アカウント情報ステータスID"
    }
    temp_prod_db_access_key_info {
        INTEGER id PK "ID"
        INTEGER FK_account_info_id FK "アカウント情報ID"
    }
    temp_prod_db_setting_info {
        INTEGER id PK "ID"
        INTEGER FK_account_info_id FK "アカウント情報ID"
    }
    temp_prod_db_account_group {
        INTEGER FK_group_info_id PK "グループ情報ID"
        INTEGER FK_account_info_id PK "アカウント情報ID"
    }
    
    temp_prod_db_group_info {
        INTEGER id PK "ID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
        STRING group_name "グループ名"
    }
    temp_prod_db_serial_info_status {
        INTEGER id PK "ID"
        STRING status "ステータス"
    }
    temp_prod_db_serial_info {
        INTEGER id PK "ID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
        STRING imei "IMEI"
    }
    temp_prod_db_serial_info_detail {
        INTEGER id PK "ID"
        INTEGER FK_serial_info_id FK "シリアル情報ID"
        INTEGER FK_serial_info_status_id FK "シリアル情報ステータスID"
    }
    temp_prod_db_serial_group {
        INTEGER FK_group_info_id PK "グループ情報ID"
        INTEGER FK_serial_info_id PK "シリアル情報ID"
    }
    
    temp_prod_db_subscription_plan_info {
        INTEGER id PK "ID"
        STRING subscription_plan_name "プラン名"
    }
    temp_prod_db_corporate_subscription_plan {
        INTEGER id PK "ID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
        INTEGER FK_subscription_plan_id FK "サブスクリプションプランID"
    }
    temp_prod_db_main_feature_info {
        INTEGER id PK "ID"
        STRING main_feature_name "メイン機能名"
    }
    temp_prod_db_sub_feature_info {
        INTEGER id PK "ID"
        INTEGER FK_main_feature_info_id FK "メイン機能情報ID"
    }
    temp_prod_db_permission_info {
        INTEGER id PK "ID"
        STRING permission_name "権限名"
    }
    temp_prod_db_feature_permission {
        INTEGER id PK "ID"
        INTEGER FK_sub_feature_info_id FK "サブ機能情報ID"
        INTEGER FK_permission_info_id FK "権限情報ID"
    }
    temp_prod_db_role_feature_permission {
        INTEGER FK_role_info_id PK "ロール情報ID"
        INTEGER FK_feature_permission_id PK "機能権限ID"
    }
    temp_prod_db_subscription_plan_feature_permission {
        INTEGER FK_subscription_plan_info_id PK "サブスクリプションプラン情報ID"
        INTEGER FK_feature_permission_id PK "機能権限ID"
    }

    temp_prod_db_remote_mode_registry {
        INTEGER id PK "ID"
        STRING mode_name "モード名"
    }
    temp_prod_db_remote_mode_value_device {
        INTEGER id PK "ID"
        INTEGER FK_remote_mode_registry_id FK "リモートモードレジストリID"
        INTEGER FK_group_info_id FK "グループ情報ID"
        INTEGER FK_serial_info_id FK "シリアル情報ID"
    }
    temp_prod_db_remote_mode_value_group {
        INTEGER id PK "ID"
        INTEGER FK_remote_mode_registry_id FK "リモートモードレジストリID"
        INTEGER FK_group_info_id FK "グループ情報ID"
    }
    temp_prod_db_remote_setting_common_device {
        INTEGER id PK "ID"
        INTEGER FK_group_info_id FK "グループ情報ID"
        INTEGER FK_serial_info_id FK "シリアル情報ID"
    }
    temp_prod_db_remote_setting_common_group {
        INTEGER id PK "ID"
        INTEGER FK_group_info_id FK "グループ情報ID"
    }
    temp_prod_db_remote_setting_wifi_device {
        INTEGER id PK "ID"
        INTEGER FK_group_info_id FK "グループ情報ID"
        INTEGER FK_serial_info_id FK "シリアル情報ID"
    }
    temp_prod_db_remote_setting_wifi_group {
        INTEGER id PK "ID"
        INTEGER FK_group_info_id FK "グループ情報ID"
    }
    temp_prod_db_remote_restriction_registry {
        INTEGER id PK "ID"
    }
    temp_prod_db_remote_restriction_value {
        INTEGER id PK "ID"
    }
    temp_prod_db_remote_delete_data {
        INTEGER id PK "ID"
        INTEGER FK_serial_info_id FK "シリアル情報ID"
    }
    temp_prod_db_remote_device_lost_mode {
        INTEGER id PK "ID"
        INTEGER FK_serial_info_id FK "シリアル情報ID"
    }
    temp_prod_db_remote_restore_factory {
        INTEGER id PK "ID"
        INTEGER FK_serial_info_id FK "シリアル情報ID"
    }

    temp_prod_db_notification_destination {
        INTEGER id PK "ID"
    }
    temp_prod_db_notification_type {
        INTEGER id PK "ID"
        STRING type "タイプ"
    }
    temp_prod_db_notification_user_type {
        INTEGER id PK "ID"
        STRING user_type "ユーザータイプ"
    }
    temp_prod_db_notification_status {
        INTEGER id PK "ID"
        STRING status "ステータス"
    }
    temp_prod_db_notification_template {
        INTEGER id PK "ID"
        INTEGER FK_notification_user_type_id FK "通知ユーザータイプID"
        INTEGER FK_notification_type_id FK "通知タイプID"
        INTEGER FK_notification_destination_id FK "通知先ID"
    }
    temp_prod_db_notification_info {
        INTEGER id PK "ID"
        INTEGER FK_notification_template_id FK "通知テンプレートID"
        INTEGER FK_notification_status_id FK "通知ステータスID"
        INTEGER FK_notification_type_id FK "通知タイプID"
        INTEGER FK_notification_user_type_id FK "通知ユーザータイプID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
        INTEGER FK_notification_destination_id FK "通知先ID"
    }
    temp_prod_db_notification_detail {
        INTEGER id PK "ID"
        INTEGER FK_notification_info_id FK "通知情報ID"
        INTEGER FK_notification_destination_id FK "通知先ID"
    }

    %% Other temporary tables (Masters/Logs/Misc)
    temp_prod_db_bo_account_info_status_color_mapping {
        INTEGER FK_bo_account_info_status_id PK "BOアカウント情報ステータスID"
        INTEGER FK_color_master_id PK "色マスターID"
    }
    temp_prod_db_bo_serial_import_history_info_status {
        INTEGER id PK "ID"
    }
    temp_prod_db_bo_serial_import_history_info_status_color_mapping {
        INTEGER id PK "ID"
    }
    temp_prod_db_bo_sku_info {
        INTEGER id PK "ID"
    }
    temp_prod_db_bo_one_time_key_info {
        INTEGER id PK "ID"
    }
    temp_prod_db_bo_account_master {
        INTEGER id PK "ID"
    }
    temp_prod_db_bo_account_info {
        INTEGER id PK "ID"
        INTEGER FK_bo_account_info_status_id FK "BOアカウント情報ステータスID"
        INTEGER FK_bo_account_master_id FK "BOアカウントマスターID"
        INTEGER FK_language_master_id FK "言語マスターID"
    }
    temp_prod_db_bo_access_key_info {
        INTEGER id PK "ID"
        INTEGER FK_bo_account_info_id FK "BOアカウント情報ID"
    }
    temp_prod_db_bo_serial_import_history_info {
        INTEGER id PK "ID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
        INTEGER FK_bo_serial_import_history_info_status_id FK "シリアルインポートステータスID"
    }
    temp_prod_db_temp_account_info {
        INTEGER id PK "ID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
        INTEGER FK_role_info_id FK "ロール情報ID"
        INTEGER FK_language_master_id FK "言語マスターID"
        INTEGER FK_account_info_status_id FK "アカウント情報ステータスID"
    }
    temp_prod_db_corporate_contact_info {
        INTEGER id PK "ID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
    }
    temp_prod_db_glossary_info {
        INTEGER id PK "ID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
    }
    temp_prod_db_translation_history_control_info {
        INTEGER id PK "ID"
        INTEGER FK_corporation_info_id FK "法人情報ID"
    }
    temp_prod_db_privacy_policy {
        INTEGER id PK "ID"
        INTEGER FK_language_master_id FK "言語マスターID"
    }
    temp_prod_db_terms_of_use {
        INTEGER id PK "ID"
        INTEGER FK_language_master_id FK "言語マスターID"
    }
    temp_prod_db_measured_value {
        INTEGER id PK "ID"
    }
    temp_prod_db_measured_translation_value {
        INTEGER id PK "ID"
    }
    temp_prod_db_one_time_key_info {
        INTEGER id PK "ID"
    }
    temp_prod_db_consent_history {
        INTEGER id PK "ID"
    }
    temp_prod_db_corporation_info_status_color_mapping {
        INTEGER FK_corporation_info_status_id PK "法人情報ステータスID"
        INTEGER FK_color_master_id PK "色マスターID"
    }
    temp_prod_db_serial_info_status_color_mapping {
        INTEGER FK_serial_info_status_id PK "シリアル情報ステータスID"
        INTEGER FK_color_master_id PK "色マスターID"
    }


    %% -----------------------------------------------------------
    %% Relationships: Global Masters (Prod)
    %% -----------------------------------------------------------
    
    prod_db_global_sql_bo_account_master ||--o{ prod_db_global_sql_bo_account_info : FK_bo_account_master_id
    prod_db_global_sql_bo_language_master ||--o{ prod_db_global_sql_bo_account_info : FK_bo_language_master_id
    prod_db_global_sql_bo_account_info_status ||--o{ prod_db_global_sql_bo_account_info : FK_bo_account_info_status_id
    prod_db_global_sql_bo_account_info ||--o{ prod_db_global_sql_bo_access_key_info : FK_bo_account_info_id
    
    prod_db_global_sql_bo_account_info_status }o--o{ prod_db_global_sql_bo_color_master : Mapping
    prod_db_global_sql_bo_corporation_info_status }o--o{ prod_db_global_sql_bo_color_master : Mapping
    
    prod_db_global_sql_engine_server_info ||--o{ prod_db_global_sql_server_region_info : FK_engine_server_info_id
    prod_db_global_sql_server_region_info }o--o{ prod_db_global_sql_sales_region_info : Mapping
    prod_db_global_sql_server_region_info ||--o{ prod_db_global_sql_master_corporation_info : FK_server_region_info_id
    prod_db_global_sql_master_corporation_info ||--o{ prod_db_global_sql_serial_info_master : FK_corp_id
    
    prod_db_global_sql_serial_info_master ||--o{ prod_db_global_sql_device_public_secret_key_info : FK_serial_info_master_id
    prod_db_global_sql_serial_info_master ||--o{ prod_db_global_sql_device_url_control_info : FK_master_serial_info_id

    prod_db_global_sql_url_type ||--o{ prod_db_global_sql_url_info : FK_url_type_id
    prod_db_global_sql_server_region_info ||--o{ prod_db_global_sql_url_info : FK_server_region_info_id

    prod_db_global_sql_master_corporation_info ||--o{ prod_db_global_sql_bo_serial_import_history_info : FK_master_corporation_info_id
    prod_db_global_sql_bo_serial_import_history_info_status ||--o{ prod_db_global_sql_bo_serial_import_history_info : FK_bo_serial_import_history_info_status_id

    %% -----------------------------------------------------------
    %% Relationships: Temporary/Operational (Temp)
    %% -----------------------------------------------------------
    
    %% Account/Role/Language/Status
    temp_prod_db_corporation_info_status ||--o{ temp_prod_db_corporation_info : Fk_corporation_info_status_id
    temp_prod_db_corporation_info ||--o{ temp_prod_db_account_info : FK_corporation_info_id
    temp_prod_db_role_info ||--o{ temp_prod_db_account_info : FK_role_info_id
    temp_prod_db_language_master ||--o{ temp_prod_db_account_info : FK_language_master_id
    temp_prod_db_account_info_status ||--o{ temp_prod_db_account_info : FK_account_info_status_id
    temp_prod_db_account_info ||--o{ temp_prod_db_access_key_info : FK_account_info_id
    temp_prod_db_account_info ||--o{ temp_prod_db_setting_info : FK_account_info_id

    %% Device/Serial/Group Management
    temp_prod_db_corporation_info ||--o{ temp_prod_db_group_info : FK_corporation_info_id
    temp_prod_db_corporation_info ||--o{ temp_prod_db_serial_info : FK_corporation_info_id
    temp_prod_db_serial_info ||--o{ temp_prod_db_serial_info_detail : FK_serial_info_id
    temp_prod_db_serial_info_status ||--o{ temp_prod_db_serial_info_detail : FK_serial_info_status_id
    temp_prod_db_group_info }o--o{ temp_prod_db_serial_info : SerialGroup
    
    temp_prod_db_serial_info ||--o{ temp_prod_db_remote_delete_data : FK_serial_info_id
    temp_prod_db_serial_info ||--o{ temp_prod_db_remote_device_lost_mode : FK_serial_info_id
    temp_prod_db_serial_info ||--o{ temp_prod_db_remote_restore_factory : FK_serial_info_id
    temp_prod_db_remote_mode_registry ||--o{ temp_prod_db_remote_mode_value_device : FK_remote_mode_registry_id
    temp_prod_db_remote_mode_registry ||--o{ temp_prod_db_remote_mode_value_group : FK_remote_mode_registry_id
    temp_prod_db_serial_info ||--o{ temp_prod_db_remote_mode_value_device : FK_serial_info_id
    temp_prod_db_group_info ||--o{ temp_prod_db_remote_mode_value_device : FK_group_info_id
    temp_prod_db_group_info ||--o{ temp_prod_db_remote_mode_value_group : FK_group_info_id
    temp_prod_db_serial_info ||--o{ temp_prod_db_remote_setting_common_device : FK_serial_info_id
    temp_prod_db_group_info ||--o{ temp_prod_db_remote_setting_common_device : FK_group_info_id
    temp_prod_db_group_info ||--o{ temp_prod_db_remote_setting_common_group : FK_group_info_id
    temp_prod_db_serial_info ||--o{ temp_prod_db_remote_setting_wifi_device : FK_serial_info_id
    temp_prod_db_group_info ||--o{ temp_prod_db_remote_setting_wifi_device : FK_group_info_id
    temp_prod_db_group_info ||--o{ temp_prod_db_remote_setting_wifi_group : FK_group_info_id

    %% Subscription/Feature/Permission
    temp_prod_db_corporation_info ||--o{ temp_prod_db_corporate_subscription_plan : FK_corporation_info_id
    temp_prod_db_subscription_plan_info ||--o{ temp_prod_db_corporate_subscription_plan : FK_subscription_plan_id
    temp_prod_db_main_feature_info ||--o{ temp_prod_db_sub_feature_info : FK_main_feature_info_id
    temp_prod_db_sub_feature_info ||--o{ temp_prod_db_feature_permission : FK_sub_feature_info_id
    temp_prod_db_permission_info ||--o{ temp_prod_db_feature_permission : FK_permission_info_id
    temp_prod_db_role_info }o--o{ temp_prod_db_feature_permission : RoleFeaturePermission

    temp_prod_db_subscription_plan_info }o--o{ temp_prod_db_feature_permission : SubscriptionPlanFeaturePermission

    %% Notification
    temp_prod_db_notification_user_type ||--o{ temp_prod_db_notification_template : FK_notification_user_type_id
    temp_prod_db_notification_type ||--o{ temp_prod_db_notification_template : FK_notification_type_id
    temp_prod_db_notification_destination ||--o{ temp_prod_db_notification_template : FK_notification_destination_id
    temp_prod_db_notification_template ||--o{ temp_prod_db_notification_info : FK_notification_template_id
    temp_prod_db_notification_status ||--o{ temp_prod_db_notification_info : FK_notification_status_id
    temp_prod_db_notification_info ||--o{ temp_prod_db_notification_detail : FK_notification_info_id
    temp_prod_db_notification_destination ||--o{ temp_prod_db_notification_detail : FK_notification_destination_id

    %% Other Temp FKs
    temp_prod_db_language_master ||--o{ temp_prod_db_language_code_master : FK_language_master_id
    temp_prod_db_language_master ||--o{ temp_prod_db_privacy_policy : FK_language_master_id
    temp_prod_db_language_master ||--o{ temp_prod_db_terms_of_use : FK_language_master_id
    temp_prod_db_corporation_info ||--o{ temp_prod_db_corporate_contact_info : FK_corporation_info_id
    temp_prod_db_corporation_info ||--o{ temp_prod_db_glossary_info : FK_corporation_info_id
    temp_prod_db_corporation_info ||--o{ temp_prod_db_translation_history_control_info : FK_corporation_info_id
    
    %% Color Mappings (Temp)
    temp_prod_db_account_info_status }o--o{ temp_prod_db_color_master : AccStatusColorMapping
    temp_prod_db_corporation_info_status }o--o{ temp_prod_db_color_master : CorpStatusColorMapping
    temp_prod_db_serial_info_status }o--o{ temp_prod_db_color_master : SerialStatusColorMapping
```