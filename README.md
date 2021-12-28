# workbook-merge

[![GitHub issues](https://img.shields.io/github/issues/iu-actions/workbook-merge)](https://github.com/iu-actions/workbook-merge/issues)

This action merges the cover page and the content of an IU Workbook.

## Found a bug? 💁‍♀️

Thanks for letting us know! Please [file an issue](../../issues/new?assignees=&labels=&template=bug_report.md&title=) and we should reply shortly.

## Configuration

This action is dependent on the [iu-actions/workbook-cover](https://github.com/iu-actions/workbook-cover) and [iu-actions/workbook-content](https://github.com/iu-actions/workbook-content) actions.

## Example

Below you will find an example of how you can use this action.

```yaml
jobs:
  cover:
    runs-on: ubuntu-latest
    steps:
      - name: Create Cover
        uses: iu-actions/workbook-cover@main
        with:
          # student details
          first_name: John
          last_name: Doe
          email: john.doe@university.edu
          id: 123456
          degree: B. Sc. Computer Science

          # course details
          course_name: Mathematics I
          course_id: 56.05J
          professor: Prof. Dr. John Doe
          tutor: Jane Doe

          # configuration details
          format_doc: .workbook/cover/format.docx
          template_doc: .workbook/cover/template.md
  content:
    runs-on: ubuntu-latest
    steps:
      - name: Create Content
        uses: iu-actions/workbook-content@main
        with:
          # workbook details
          workbook: exam/workbook.md

          # configuration details
          format_doc: .workbook/content/format.docx
  merge:
    needs: [cover, content]
    runs-on: ubuntu-latest
    steps:
      - name: Merge (Cover, Content)
        uses: iu-actions/workbook-merge@main
  ```
