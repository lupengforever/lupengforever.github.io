!>注意：timestamps(created_at、updated_at)、deleted_at 表示创建、修改、创建时间

## banner

表名 banners (timestamps)

| 字段名      | 类型             | 是否为空 | 描述                                   |
| ----------- | ---------------- | -------- | -------------------------------------- |
| id          | int(10) unsigned | NO       | PRI                                    |
| type        | tinyint(4)       | NO       | 类型 1 校圈 2 云课堂 3 发现 4 生活精选 |
| sender_type | tinyint(4)       | NO       | 发送人类型                             |
| sender      | varchar(191)     | YES      | 发送人部门显示                         |
| title       | varchar(191)     | YES      | 轮播图标题                             |
| weight      | int(11)          | NO       | 权重                                   |
| user_id     | int(11)          | NO       | 用户 id                                |
| link_url    | varchar(255)     | YES      | 链接地址                               |
| image_url   | varchar(255)     | NO       | 链接地址                               |
| content     | text             | YES      | 描述内用                               |

```php
    class{
        user:belongsTo();//发布者
    }
```

## 班级

表名 clazzs (timestamps)

| 字段名          | 类型    | 描述                |
| --------------- | ------- | ------------------- |
| id              | int     | 班级编号 `index`    |
| school_id       | varchar | 学校编号 `for-key`  |
| department_id   | int     | 专业编号 `for-key`  |
| department_code | varchar | 学院编号 `sync`     |
| major_id        | varchar | 专业编号 `for-key`  |
| major_code      | varchar | 专业编号 `sync`     |
| clazz_code      | varchar | 班级编号 `sync`     |
| total_count     | varchar | 共计多少人          |
| name            | varchar | 班级名              |
| year            | varchar | 开班年份            |
| educate_year    | int     | 学制                |
| user_id         | int     | 辅导员 id `for-key` |
| hash            | varchar | `uni`               |

```php
    class{
        department:belongsTo();//学院
        major:belongsTo();//专业
        students:hasMany();//专业
    }
```

## 课程详情

表名 course_infos (timestamps)

| 字段名             | 类型             | 是否为空 | 描述                |
| ------------------ | ---------------- | -------- | ------------------- |
| id                 | int(10) unsigned | NO       | PRI                 |
| school_id          | int(11)          | NO       |                     |
| original_key       | varchar(191)     | YES      | 序号                |
| course_info_code   | varchar(191)     | YES      | 课程编号 `sync`     |
| course_info_detail | varchar(191)     | YES      | 课程编号 `sync`     |
| name               | varchar(191)     | YES      | 名称                |
| department_id      | varchar(191)     | YES      | 院系编号 `for-key`  |
| department_code    | varchar(191)     | YES      | 院系编号 `sync`     |
| year               | varchar(191)     | YES      | 学年                |
| term               | varchar(191)     | YES      | 学期                |
| course_count       | varchar(191)     | YES      | 总学时              |
| score              | varchar(191)     | YES      | 学分                |
| course_type1       | varchar(191)     | YES      | 课程类别            |
| course_type2       | varchar(191)     | YES      |                     |
| exam_type          | varchar(191)     | YES      | 考核方式            |
| teacher_info_id    | int(11)          | YES      | 老师详情编号        |
| teacher_info_code  | varchar(191)     | YES      | 老师详情编号 `sync` |
| total_count        | varchar(20)      | YES      | 人数                |
| singlecourse_count | varchar(20)      | YES      | 单次节数            |
| schedule           | longtext         | YES      | 课表详情            |
| teacher_name       | varchar(191)     | YES      | 老师名称            |
| schedule_time      | longtext         | YES      |                     |
| schedule_location  | longtext         | YES      |                     |
| schedule_type      | tinyint(4)       | NO       |                     |
| status             | tinyint(4)       | YES      | 开课状态            |
| hash               | varchar(33)      | NO       | 字符串 hash 值      |

```php
    class{
        course:hasOne();//课程信息
        department:belongsTo();//学院
    }
```

## 课程通知

表名 course_marks (timestamps、deleted_at)

| 字段名    | 类型             | 是否为空 | 描述               |
| --------- | ---------------- | -------- | ------------------ |
| id        | int(10) unsigned | NO       | PRI                |
| course_id | int(11)          | NO       | 课程 `for-key`     |
| mark_id   | int(11)          | NO       | 评价标签 `for-key` |

## 课程通知

表名 course_notices (timestamps)

| 字段名    | 类型             | 是否为空 | 描述           |
| --------- | ---------------- | -------- | -------------- |
| id        | int(10) unsigned | NO       | PRI            |
| user_id   | int(11)          | NO       | 用户 `for-key` |
| title     | varchar(191)     | NO       | 标题           |
| content   | longtext         | YES      | 内容           |
| course_id | int(11)          | NO       | 课程 `for-key` |
| type      | tinyint(4)       | NO       | 类型           |

```php
    class{
        user:belongsTo();//用户
    }
```

## 课程进度

表名 course_schedule_interactions (timestamps)

| 字段名             | 类型             | 是否为空 | 描述                |
| ------------------ | ---------------- | -------- | ------------------- |
| id                 | int(10) unsigned | NO       | PRI                 |
| course_id          | int(10)          | YES      | 课程 `for-key`      |
| course_schedule_id | int(11)          | NO       | 课程进度 `for-key`  |
| title              | longtext         | YES      | 标题                |
| image              | json             | YES      | 图片                |
| extra              | json             | YES      | 其他                |
| from               | int(10)          | YES      | 来源-》进度         |
| teacher_id         | int(10)          | YES      | 教师 `for-key`      |
| status             | tinyint(4)       | YES      | 状态 0 待 1 已 2 隐 |

```php
    class{
        from:belongsTo();//来源进度
        schedule:belongsTo();//进度
        course:belongsTo();//课程
    }
```

## 课程进度

表名 course_schedule (timestamps)

| 字段名            | 类型             | 是否为空 | 描述           |
| ----------------- | ---------------- | -------- | -------------- |
| id                | int(10) unsigned | NO       | PRI            |
| course_id         | int(11)          | NO       | `for-key`      |
| week_num          | tinyint(4)       | NO       | 周次           |
| day_of_week       | tinyint(4)       | NO       | 周几           |
| course_count      | varchar(191)     | NO       | 共计多少节     |
| status            | tinyint(4)       | NO       | 状态           |
| intraction_status | tinyint(4)       | NO       | 话题讨论状态   |
| position          | varchar(191)     | YES      | 位置           |
| extra             | json             | YES      | 其他信息       |
| avg               | decimal(4,2)     | NO       | 教学评价平均分 |

```php
    class{
        courses:belongsTo();//课程信息
        marks:belongsToMany();//教学评价标签
        evaluates:hasMany();//教学评价
        interactions:hasMany();//互动
    }
```

## 课程学生关系表

表名 course_student

| 字段名      | 类型             | 是否为空 | 描述      |
| ----------- | ---------------- | -------- | --------- |
| id          | int(10) unsigned | NO       | PRI       |
| course_id   | int(11)          | NO       | `for-key` |
| student_id  | int(11)          | NO       | `for-key` |
| hash        | varchar(65)      | YES      | UNI       |
| small_group | tinyint(4)       | NO       | 分组      |

## 课程

表名 courses (timestamps)

| 字段名             | 类型             | 是否为空 | 描述                         |
| ------------------ | ---------------- | -------- | ---------------------------- |
| id                 | int(10) unsigned | NO       | PRI                          |
| name               | varchar(191)     | YES      |                              |
| course_info_id     | int(11)          | NO       | `for-key`                    |
| course_info_detail | varchar(191)     | YES      | 原始编码 `sync`              |
| school_id          | int(11)          | NO       | `for-key`                    |
| teacher_info_id    | varchar(191)     | YES      | 教师详情 `for-key`           |
| teacher_name       | varchar(191)     | YES      | 教师姓名                     |
| year               | varchar(191)     | YES      | 学年                         |
| term               | varchar(191)     | YES      | 学期                         |
| schedule           | longtext         | YES      | 课表进度详情                 |
| extra              | json             | YES      | 其他信息                     |
| hash               | varchar(65)      | NO       | UNI                          |
| schedule_time      | longtext         | YES      |                              |
| schedule_location  | longtext         | YES      |                              |
| status             | tinyint(4)       | YES      | 是否开课                     |
| schedule_type      | tinyint(4)       | NO       | 进度类型(不同学校可能不一样) |
| describe           | text             | YES      | 描述、要求                   |

```php
    class{
        students:belongsToMany();//学生
        teacherInfo:belongsTo();//教师详情
        courseInfo:belongsTo();//课程详情
        attendances:hasMany();//考勤
        exams:hasMany();//测验
        courseNotices:hasMany();//课程通知
        courseSchedules:hasMany();//课程进度
        labels:belongsToMany();//？？
        label:hasMany();//？？
        marks:belongsToMany();//教学评价标签
        coursewares:hasMany();//课件
        courseInteractions:hasMany();//课堂互动
        qss:hasMany();//问卷
        homeworks:hasMany();//作业
        syncShow:hasMany();//同步放映
    }
```

## 课件

表名 coursewares

| 字段名      | 类型             | 是否为空 | 描述           |
| ----------- | ---------------- | -------- | -------------- |
| id          | int(10) unsigned | NO       | PRI            |
| teacher_id  | int(11)          | NO       | 教师 `for-key` |
| course_id   | int(11)          | NO       | 课程 `for-key` |
| url         | varchar(191)     | YES      | link           |
| 3rd_url     | varchar(191)     | YES      | 外部 link      |
| type        | tinyint(4)       | NO       | 类型           |
| suffix      | varchar(20)      | NO       | 后缀           |
| size        | varchar(20)      | YES      | 大小           |
| name        | varchar(191)     | NO       | 名字           |
| description | longtext         | YES      | 描述           |
| from        | int(10)          | YES      | 来源           |
| sync_url    | varchar(255)     | YES      | 同步放映       |

```php
    class{
        homeworks:belongsToMany();//作业
        course:belongsTo();//课程
        teacher:belongsTo();//教师
    }
```

## 学院

表名 departments (timestamps)

| 字段名          | 类型    | 描述               |
| --------------- | ------- | ------------------ |
| id              | int     | 学院编号 `index`   |
| school_id       | tinyint | 学校编号 `for-key` |
| name            | varchar | 学院中文名         |
| department_code | varchar | 学院编号 `sync`    |

```php
    class{
        exam:belongsTo();//测验
        student:belongsTo();//学生
    }
```

## 测验题

表名 exam_questions (timestamps)

| 字段名      | 类型             | 是否为空 | 描述           |
| ----------- | ---------------- | -------- | -------------- |
| exam_id     | int(10) unsigned | NO       | 测验 `for-key` |
| question_id | int(10) unsigned | NO       | 题             |

## 测验上交情况

表名 exam_scores (timestamps、deleted_at)

| 字段名     | 类型             | 是否为空 | 描述 |
| ---------- | ---------------- | -------- | ---- |
| id         | int(10) unsigned | NO       | PRI  |
| exam_id    | int(10) unsigned | NO       |      |
| student_id | int(10) unsigned | NO       |      |
| answer     | json             | YES      |      |
| score      | int(11)          | NO       |      |

```php
    class{
        examScores:hasMany();//上交情况
        students:belongsToMany();//学生
        questions:belongsToMany();//题
        course:belongsTo();//课程
    }
```

## 测验

表名 exams (timestamps、deleted_at)

| 字段名                | 类型             | 是否为空 | 描述                                            |
| --------------------- | ---------------- | -------- | ----------------------------------------------- |
| id                    | int(10) unsigned | NO       | PRI                                             |
| exam_type             | tinyint(4)       | NO       | 类型                                            |
| course_id             | int(11)          | NO       | 课程 `for-key`                                  |
| teacher_id            | int(10) unsigned | NO       | 教师 `for-key`                                  |
| total_question        | tinyint(4)       | NO       | 共多少题                                        |
| total_score           | tinyint(4)       | NO       | 共多少分                                        |
| publish_answer_type   | tinyint(4)       | NO       | 公布答案类型 1 自动公布，0 手动公布，2 作答完成 |
| publish_answer_status | tinyint(4)       | NO       | 公布答案状态 1 未公布 2 已公布(自动公布也是 2)  |
| title                 | varchar(255)     | YES      | 标题                                            |
| start_time            | timestamp        | YES      | 开始时间                                        |
| end_time              | timestamp        | YES      | 结束时间                                        |
| extra                 | json             | YES      | 其他                                            |
| allow_answer_user_num | int(11)          | NO       | 作答人数                                        |
| status                | tinyint(4)       | YES      | 状态                                            |
| duration              | int(10)          | YES      | 持续时长                                        |
| from                  | int(10)          | YES      | 来源                                            |

```php
    class{
        examScores:hasMany();//上交情况
        students:belongsToMany();//学生
        questions:belongsToMany();//题
        course:belongsTo();//课程
    }
```

## 学生上交作业表

表名 hand_in_homeworks (timestamps、deleted_at)

| 字段名       | 类型             | 是否为空 | 描述                |
| ------------ | ---------------- | -------- | ------------------- |
| id           | int(10) unsigned | NO       | PRI                 |
| student_id   | int(11)          | NO       | 学生 `for-key`      |
| homework_id  | int(11)          | NO       | 作业 `for-key`      |
| course_id    | int(11)          | NO       | 课程 `for-key`      |
| url          | varchar(191)     | YES      | 课件 url            |
| status       | int(11)          | NO       |                     |
| score        | varchar(191)     | NO       | 得分                |
| answer       | json             | YES      | 答案                |
| reply_status | tinyint(4)       | YES      | 批复状态 true false |
| group        | tinyint(4)       | YES      | 小组                |

```php
    class{
        homework:belongsTo();//作业情况
        students:belongsTo();//学生
    }
```

## 作业题关系表

表名 homework_question (timestamps)

| 字段名      | 类型             | 是否为空 | 描述           |
| ----------- | ---------------- | -------- | -------------- |
| homework_id | int(10) unsigned | NO       | 作业 `for-key` |
| question_id | int(10) unsigned | NO       | 题 `for-key`   |

## 作业

表名 homeworks (timestamps、deleted_at)

| 字段名                | 类型             | 是否为空 | 描述 |
| --------------------- | ---------------- | -------- | ---- |
| id                    | int(10) unsigned | NO       | PRI  |
| teacher_id            | int(11)          | NO       | MUL  |
| course_id             | int(11)          | NO       | MUL  |
| title                 | varchar(191)     | NO       |      |
| 3rd_url               | varchar(191)     | YES      |      |
| url                   | json             | YES      |      |
| type                  | tinyint(4)       | NO       |      |
| group_type            | tinyint(4)       | NO       |      |
| description           | longtext         | YES      |      |
| begin_time            | timestamp        | YES      |      |
| end_time              | timestamp        | YES      |      |
| from                  | int(10)          | YES      |      |
| repair_time           | timestamp        | YES      |      |
| allow_answer_user_num | int(10)          | YES      |      |
| reply_num             | int(10)          | YES      |      |

```php
    class{
        handInHomeworks:hasMany();//作业上交情况
        coursewares:belongsToMany();//课件
        teachers:belongsTo();//教师
        course:belongsTo();//课程
        // notification:morphOne();//通知
        questions:belongsToMany();//题
        students:belongsToMany();//学生
        from:belongsTo();//来源
    }
```

## 专业

表名 majors (timestamps)

| 字段名           | 类型    | 描述               |
| ---------------- | ------- | ------------------ |
| id               | int     | 专业编号 `index`   |
| major_code       | varchar | 专业编号 `sync`    |
| school_id        | int     | 学校编号 `for-key` |
| department_id    | varchar | 学院编号           |
| department_code  | varchar | 学院编号 `sync`    |
| educate_year     | varchar | 学制               |
| major_start_year | varchar | 开始时间           |
| extra            | json    | 其他               |
| hash             | varchar | `uni`              |

```php
    class{
        school:belongsTo();//学校
        department:belongsTo();//学院
    }
```

## 云课堂相关通知表

表名 notifications (timestamps、deleted_at)

| 字段名        | 类型                | 是否为空 | 描述           |
| ------------- | ------------------- | -------- | -------------- |
| id            | int(10) unsigned    | NO       | PRI            |
| course_id     | int(10)             | YES      | 课程 `for-key` |
| from_id       | bigint(20)          | NO       | 来源 `for-key` |
| from_type     | varchar(191)        | NO       | 来源类型       |
| role_id       | int(11)             | NO       | 接收这类型     |
| type          | tinyint(4)          | NO       | `参考配置`     |
| relative_type | varchar(191)        | NO       | 主模型         |
| relative_id   | bigint(20) unsigned | NO       | 主模型 id      |
| content       | varchar(255)        | YES      | 内容           |
| status        | tinyint(4)          | YES      | 阅读状态       |

```php
    class{
        from:morphTo();//来源
        relative:morphTo();//主模型信息
        course:belongsTo();//课程
    }
```

## 问卷

表名 qss (timestamps、deleted_at)

| 字段名                | 类型             | 是否为空 | 描述           |
| --------------------- | ---------------- | -------- | -------------- |
| id                    | int(10) unsigned | NO       | PRI            |
| exam_type             | tinyint(4)       | NO       |                |
| course_id             | int(11)          | NO       | 课程 `for-key` |
| teacher_id            | int(10) unsigned | NO       | 教师 `for-key` |
| total_question        | tinyint(4)       | NO       | 共多少题       |
| total_score           | tinyint(4)       | NO       | 共多少分       |
| publish_answer_type   | tinyint(4)       | NO       | `同测验`       |
| publish_answer_status | tinyint(4)       | NO       | `同测验`       |
| title                 | varchar(255)     | YES      | 标题           |
| start_time            | timestamp        | YES      | 开始时间       |
| end_time              | timestamp        | YES      | 结束时间       |
| extra                 | json             | YES      | 其他           |
| allow_answer_user_num | int(11)          | NO       | 作答人数       |
| status                | tinyint(4)       | YES      |                |
| duration              | int(10)          | YES      | 持续时长       |
| from                  | int(10)          | YES      | 来源           |

```php
    class{
        course:belongsTo();//课程
        questions:belongsToMany();//题
        qsScores:hasMany();//上交情况
        students:belongsToMany();//学生
    }
```

## 问卷题关系表

表名 qs_qs_question (timestamps)

| 字段名         | 类型             | 是否为空 | 描述           |
| -------------- | ---------------- | -------- | -------------- |
| qs_id          | int(10) unsigned | NO       | 问卷 `for-key` |
| qs_question_id | int(10) unsigned | NO       | 题 `for-key`   |

## 问卷题

表名 qs_qs_question (timestamps、deleted_at)

| 字段名           | 类型             | 是否为空 | 描述                           |
| ---------------- | ---------------- | -------- | ------------------------------ |
| id               | int(10) unsigned | NO       | PRI                            |
| course_id        | int(10) unsigned | NO       | 课程 `for-key`                 |
| teacher_id       | int(10)          | YES      | 教师 `for-key`                 |
| question_source  | tinyint(4)       | NO       |                                |
| has_score        | tinyint(4)       | NO       | 是否有分                       |
| score            | tinyint(4)       | YES      | 分值                           |
| type             | tinyint(4)       | NO       | 题类型 0 单 1 多 2 判断 3 主观 |
| must_filled      | tinyint(4)       | NO       | 是否必答 1 必答 0 非必答       |
| content          | longtext         | YES      | 题干                           |
| imgs             | text             | YES      | 题干图片链接                   |
| choices          | json             | YES      | 选项                           |
| right_answer     | json             | YES      | 正确答案                       |
| reference_answer | text             | YES      | 参考答案                       |
| from             | int(10)          | YES      | 来源于课程 id                  |
| from_type        | tinyint(4)       | YES      | 来源类型 0 创建 1 导入         |

```php
    class{
        qs:belongsToMany();//问卷
        course:belongsTo();//课程
        from:belongsTo();//来源
    }
```

## 作业、测验题

表名 questions (timestamps、deleted_at)

| 字段名           | 类型             | 是否为空 | 描述 |
| ---------------- | ---------------- | -------- | ---- |
| id               | int(10) unsigned | NO       | PRI  |
| teacher_id       | int(10)          | YES      |      |
| course_id        | int(10) unsigned | NO       |      |
| question_source  | tinyint(4)       | NO       |      |
| has_score        | tinyint(4)       | NO       |      |
| score            | tinyint(4)       | YES      |      |
| type             | tinyint(4)       | NO       |      |
| must_filled      | tinyint(4)       | NO       |      |
| content          | longtext         | YES      |      |
| imgs             | text             | YES      |      |
| choices          | json             | YES      |      |
| right_answer     | json             | YES      |      |
| reference_answer | text             | YES      |      |
| from             | int(10)          | YES      |      |
| from_type        | tinyint(4)       | YES      |      |

## 课程进度评价语关系表

表名 schedule_marks (timestamps、deleted_at)

| 字段名      | 类型             | 是否为空 | 描述      |
| ----------- | ---------------- | -------- | --------- |
| id          | int(10) unsigned | NO       | PRI       |
| schedule_id | int(11)          | NO       | `for-key` |
| mark_id     | int(11)          | NO       | `for-key` |
| avg         | decimal(4,2)     | NO       | 平均分    |

## 校园通知（动态校园）

表名 school_notices (timestamps、deleted_at)

| 字段名       | 类型                | 是否为空 | 描述                |
| ------------ | ------------------- | -------- | ------------------- |
| id           | int(10) unsigned    | NO       | PRI                 |
| title        | varchar(191)        | NO       | 公告标题            |
| from         | varchar(191)        | NO       | 消息来源            |
| to_type      | json                | NO       | 指定对象            |
| type         | tinyint(4)          | NO       | 消息类型            |
| user_id      | int(11)             | YES      | 发布者 `for-key`    |
| content      | longtext            | YES      | 内容                |
| extra        | json                | YES      | 预留                |
| sort         | int(11)             | NO       | 权重                |
| url_name     | varchar(191)        | YES      | 链接名称            |
| url          | varchar(191)        | YES      | 链接地址            |
| jump_type    | varchar(191)        | YES      | MUL                 |
| jump_id      | bigint(20) unsigned | YES      |                     |
| presended_at | timestamp           | YES      | 预定发送时间        |
| status       | tinyint(4)          | NO       |                     |
| top          | tinyint(4)          | NO       | 是否置顶 true false |

```php
    class{
        extedModel:morphTo();//jump
        schoolNoticeType:belongsTo();//类型
    }
```

## 学校

表名 schools (timestamps)

| 字段名     | 类型    | 描述             |
| ---------- | ------- | ---------------- |
| id         | int     | 学校编号 `index` |
| eng        | varchar | 学校名拼音       |
| name       | varchar | 学校中文名       |
| connection | varchar | 校方数据连接名   |

```php
    class{
        departments:hasMany();//学院
    }
```

## 学生

表名 students (timestamps)

| 字段名             | 类型             | 是否为空 | 描述                   |
| ------------------ | ---------------- | -------- | ---------------------- |
| id                 | int(10) unsigned | NO       | 学生编号 id            |
| user_id            | int(11)          | YES      | 用户 id `for-key`      |
| jw_login_user_name | varchar(191)     | YES      | 学生教务账号           |
| name               | varchar(191)     | YES      | 姓名                   |
| school_id          | int(11)          | YES      | 学校 id `for-key`      |
| clazz_id           | int(11)          | YES      | 班级 id `for-key`      |
| student_info_id    | int(11)          | NO       | 学生信息 id `for-key`  |
| gender             | varchar(191)     | YES      | 性别                   |
| birth_day          | varchar(191)     | YES      | 生日                   |
| extra              | json             | YES      | 其他信息               |
| synced_at          | timestamp        | YES      | 信息同步时间           |
| year               | varchar(191)     | YES      | 入学年份               |
| student_info_code  | varchar(191)     | YES      | 学生信息编号 `for-key` |
| hash               | varchar(65)      | NO       | uni                    |

```php
    class{
        courses:belongsToMany();//课程信息
        attendances:belongsToMany();//考情信息
        schedules:hasMany();//课程进度信息
        user:morphOne();//用户信息
        examScores:hasMany();//测验信息
        qsScores:hasMany();//问卷信息
        courseEvaluate:hasMany();//课程评价信息
        leaveInfos:hasMany();//请假信息
        handinhomeworks:hasMany();//课程作业信息
        studentInfo:belongsTo();//学生详情
        clazz:belongsTo();//班级信息
        exams:belongsToMany();//测验
    }
```

## 学生详情

表名 student_infos (timestamps)

| 字段名            | 类型             | 是否为空 | 描述                |
| ----------------- | ---------------- | -------- | ------------------- |
| id                | int(10) unsigned | NO       | PRI                 |
| school_id         | int(11)          | NO       | 学校                |
| username          | varchar(20)      | YES      | 教务账号            |
| password          | varchar(65)      | YES      | 教务密码            |
| student_info_code | varchar(191)     | YES      | 学生信息编号 `sync` |
| year              | varchar(191)     | YES      | 入学年份            |
| clazz_id          | varchar(191)     | YES      | 班级编号 `for-key`  |
| clazz_code        | varchar(191)     | YES      | 原始班级编码 `sync` |
| name              | varchar(191)     | YES      | 姓名                |
| cardcode          | varchar(30)      | YES      | 身份证号            |
| gender            | varchar(20)      | YES      | 性别                |
| birth_day         | varchar(30)      | YES      | 生日                |
| source_school     | varchar(191)     | YES      | 生源地              |
| address           | varchar(191)     | YES      | 地址                |
| zipcode           | varchar(191)     | YES      | 邮政编码            |
| contacts          | varchar(191)     | YES      | 联系方式            |
| entry_score       | varchar(191)     | YES      | 入学成绩            |
| entry_date        | varchar(191)     | YES      | 入学时间            |
| entry_major       | varchar(191)     | YES      | 入学专业            |
| entry_phone       | varchar(191)     | YES      | 入学手机号          |
| hash              | varchar(33)      | NO       | 字符串 hash 值 UNI  |
| created_at        | timestamp        | YES      |                     |
| updated_at        | timestamp        | YES      |                     |

```php
    class{
        student:hasOne();//学生信息
    }
```

## 教师

表名 teachers (timestamps)

| 字段名          | 类型             | 是否为空 | 描述 |
| --------------- | ---------------- | -------- | ---- |
| id              | int(10) unsigned | NO       | PRI  |
| school_id       | int(11)          | YES      | MUL  |
| user_id         | int(11)          | YES      | MUL  |
| name            | varchar(191)     | YES      |      |
| teacher_info_id | int(11)          | YES      | MUL  |
| extra           | json             | YES      |      |
| department_id   | varchar(191)     | YES      | MUL  |
| gender          | varchar(191)     | YES      |      |
| synced_at       | timestamp        | YES      |      |
| hash            | varchar(65)      | NO       | UNI  |
| created_at      | timestamp        | YES      |      |
| updated_at      | timestamp        | YES      |      |

```php
    class{
        user:hasOne();//用户信息
        coursewares:hasMany();//课件
        syncShow:hasMany();//同步放映
        homeworks:hasMany();//课程作业
        exams:hasMany();//课程测验
        qss:hasMany();//课程问卷
        scheduleInteractions:hasMany();//课程进度话题讨论
        teacherInfo:belongsTo();//教师详情
        department:belongsTo();//学院
        roles:morphToMany();//角色
    }
```

## 用户

表名 users (timestamps)

| 字段名        | 类型    | 描述                  |
| ------------- | ------- | --------------------- |
| id            | int     | 用户编号 `index`      |
| phone         | varchar | 手机号                |
| nick_name     | varchar | 昵称                  |
| password      | varchar | 登录密码              |
| email         | varchar | 邮箱                  |
| name          | varchar | 名字                  |
| avatar        | varchar | 头像                  |
| group_id      | int     |                       |
| school_id     | int     | 学校 `for-key`        |
| type          | varchar | 类型                  |
| verified_code | int     | 工号                  |
| morph_type    | varchar | 关联模型              |
| morph_id      | int     | 关联模型 id `for-key` |
| grade_class   | varchar | 班级名                |
| male          | tinyint | 性别                  |
| identity_id   | varchar | 身份证号              |
| invite_code   | varchar | 邀请码                |
| status        | tinyint | 状态                  |
| im_md5        | tinyint | 网易 密码             |
| openid        | tinyint | 微信相关              |
| unionid       | tinyint | 微信相关              |

```php
    class{
        groups:belongsToMany();//分组
        department:belongsTo();//学院 ？未用状态
        fans:hasMany();//粉丝
        focus:hasMany();//关注
        moments:hasMany();//校圈
        school:belongsTo();//学校
        student:relativeRole();//学生
        teacher:relativeRole();//老师
        comments:hasMany();//评论
        activities:belongsToMany();//评论
    }
```
