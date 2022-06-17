# テーブル構成


## マスタ
- M_Users
  - id
  - name
  - pass
  - mail

- M_skills
  - id
  - name
  - skill_category_id

- M_skill_categories
  - id
  - name
  
- M_level
  - id
  - level
  - boder_line

## トランザクション
- T_studies
  - id
  - user_id
  - date
  - time
  - category_id
  - update_at()
  - update_user()

ユーザー/カテゴリ別蓄積学習時間
- T_total_study_times
  - user_id
  - skill_id
  - level_id
  - total_time

- 
## レベルアップ