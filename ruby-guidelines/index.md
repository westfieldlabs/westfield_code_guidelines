---
title: Ruby Guidelines
resource_prefix: ../
---

# Ruby guidelines

Please consult the following [ruby-style-guide](https://github.com/bbatsov/ruby-style-guide) for general guidelines.

The following are a collection of Westfield specific coding guidelines:

* <a name="line-wrapping"></a>Long lines should be wrapped at 100 columns. When wrapping chained method calls, the method should be placed on a new line with the dot preceding it and indented by two spaces.<sup>[[link](#line-wrapping)]</sup>

  ```ruby
  # bad - line is too long
  allow(ParkingActivityProcessor).to receive(:new).with(hash_including(params.slice(:access_device, :activity_type, :activity_at))).and_return(processor)

  # good - line is wrapped
  allow(ParkingActivityProcessor).to receive(:new)
    .with(hash_including(params.slice(:access_device, :activity_type, :activity_at)))
    .and_return(processor)
  ```

  String literals should be wrapped using the `\` operator:

  ```ruby
  # bad - line is too long
  error_message = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud"

  # good - line is wrapped
  error_message = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor" \
                  " incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud"
  ```

* <a name="spaces-for-indentation"></a>Use 2 spaces for indentation, no tabs.<sup>[[link](#spaces-for-indentation)]</sup>

  ```ruby
  # bad - too many spaces
  def require_app_access_token
      unless incoming_access_token_info.has_permissions?
          render_error_response(
              key: 'access_token',
              message: "has insufficient permissions for the requested endpoint",
              status: :unauthorized
          )
      end
  end

  # good - 2 spaces indentation
  def require_app_access_token
    unless incoming_access_token_info.has_permissions?
      render_error_response(
        key: 'access_token',
        message: "has insufficient permissions for the requested endpoint",
        status: :unauthorized
      )
    end
  end
  ```
